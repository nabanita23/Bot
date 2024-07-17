import React, {useEffect, useRef} from "react";
import {Container} from "react-bootstrap";
import PageNavigation from "~components/Navigation/PageNavigation";
import TaskStepper from "~components/Stepper/TaskStepper";
import PageWrapper from "~components/Wizard/PageWrapper";
import Slider from "~components/Wizard/slider/Slider";
import SliderChild from "~components/Wizard/slider/SliderChild";
import {setNavigationMetadata} from "~components/statemanagement/slices/NavigationSlice";
import {useAppDispatch, useAppSelector} from "~components/statemanagement/hooks";
import {elementSelector} from "~components/statemanagement/selectors";
import {WizardElementType} from "~components/interfaces/WizardTypes";
import Title from "~components/Header/Title";
import WorkflowStepper from "~components/Header/WorkflowStepper";
import {deleteSession, sendSessionHeartbeat} from "~components/service/SessionHeartbeatService";
import {DEFAULT_NAMESPACE} from "~components/BuilderUtils/Constants";
import {AccessMode} from "~components/interfaces/WorkflowInterface";
import { Alert } from "@connectcore/connect-components-react";
import InactivityDetector from "~components/Wizard/InactivityDetector";

const Wizard = () => {

  const {categoryMapping, elementMapping, pageMapping, elements} = useAppSelector(state => elementSelector(state));
  const {mode, wizardUpdateState} = useAppSelector(state => state.accessStore);
  const page = useAppSelector(state => state.navigationStore.page);

  const {namespace, processDefId} = useAppSelector(state => state.workflowStore, (a, b) => ((a?.namespace ?? '') + a.processDefId) === ((b?.namespace ?? '') + b.processDefId));

  const dispatch = useAppDispatch();

  const timerRef = useRef<any>();

  // Capture heartbeat
  useEffect(() => {
    const sessionId = (namespace ?? DEFAULT_NAMESPACE) + '-' + processDefId;
    timerRef.current = setInterval(() => sendSessionHeartbeat(sessionId, mode === AccessMode.READ_ONLY)
      .catch((e) => console.error(e)), 30000);

    // Remove lock on unmount
    return () => {
      if (timerRef.current) clearInterval(timerRef.current);
      deleteSession(sessionId, mode === AccessMode.READ_ONLY).catch((e) => console.error(e));
    };
  }, [namespace, processDefId, mode]);

  useEffect(() => {
    // Dummy page attribute passed
    dispatch(setNavigationMetadata({categoryMapping, elementMapping, pageMapping, page: 100000000000}));
  }, [categoryMapping, elementMapping, pageMapping, elements, wizardUpdateState, dispatch]);

  return (
    <Container fluid className="d-flex flex-column justify-content-end px-0" style={{width: '100vw', height: '100vh'}}>
      {mode !== AccessMode.EDIT && (
        <Alert kind="info" className="w-100">
          You are viewing the workflow in preview (read-only) mode
        </Alert>
      )}

      {mode === AccessMode.EDIT && <InactivityDetector />}

      <WorkflowStepper />
      <Title />
      <Container fluid className="d-flex justify-content-between flex-fill p-0" style={{overflowY: 'auto'}}>
        <TaskStepper showForElements={[WizardElementType.TASK_CONFIG, WizardElementType.FORM]} />
        <Slider>
          {elements.map((element, idx) => (
            <SliderChild key={`${wizardUpdateState}-${element.type}-${idx}`} index={page}>
              <PageWrapper
                index={idx}
                elementType={element?.type}
                category={element?.metadataProps?.category}
                childProps={element?.elementProps}
              />
            </SliderChild>
          ))}
        </Slider>
      </Container>
      <PageNavigation totalPages={elements.length} />
    </Container>
  );
};

export default Wizard;
