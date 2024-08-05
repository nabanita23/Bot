import {
  AppContainer,
  Form,
  FormDateSelector,
  FormRadioGroup,
  FormSelect,
} from '@connectcore/connect-components-react'
import { useQuery } from '@tanstack/react-query'
import { isValid } from 'date-fns'
import { useEffect, useState } from 'react'
import { batch } from 'react-redux'
import { NavDataValue } from '~components/interfaces/WorkflowInterface'
import { useAppDispatch, useAppSelector } from '~components/statemanagement/hooks'
import { setFormFields, setFormOrigin } from '~components/statemanagement/slices/WorkflowSlice'
import { stringToDate } from '~service/Util'
import { getDocumentOptions } from '~service/WorkflowService'
import { commonReactQueryParams } from '~service/Util'
import {
  documentStatusOptions,
  physicalStatusOptions,
  processStatusOptions,
  trackingStatusOptions,
} from './Options'
import './customform.scss'

const FormBodyRenderer = () => {
  const navData = useAppSelector(state => state.workflowStore.navData);
  const { formData } = useAppSelector(state => state.workflowStore.form);
  const dispatch = useAppDispatch();

  const { isSuccess, data, } = useQuery(
    ['fetchDocSection', navData?.[NavDataValue.ENTITY_CODE]],
    () => getDocumentOptions({ endPointSlug: 'form/fetchDocSection', payload: { entityCode: navData?.[NavDataValue.ENTITY_CODE] } }),
    {...commonReactQueryParams, enabled: !!navData?.[NavDataValue.ENTITY_CODE]}
  )

  const [options, setOptions] = useState({
    docSection: [],
    docCode: [],
    docVersion: [],
    docStatus: documentStatusOptions,
    physicalStatus: physicalStatusOptions,
    processStatus: processStatusOptions,
    trackingStatus: trackingStatusOptions,
  })

  const waiveRequestData = [
    { value: 'yes', text: 'Yes' },
    { value: 'no', text: 'No' },
  ]

  const creditUseData = [
    { value: 'yes', text: 'Yes' },
    { value: 'no', text: 'No' },
  ]

  useEffect(() => {
    dispatch(setFormOrigin({ formOrigin: 'capture' }))
  }, [])

  useEffect(() => {
    if (isSuccess) fetchDocSectionOptions()
  }, [isSuccess, data])

  const clearOptions = level => {
    if (level === 2) {
      batch(() => {
        dispatch(setFormFields({ formData: { docCode: { value: '', label: '' } } }))
        dispatch(setFormFields({ formData: { docVersion: { value: '', label: '' } } }))
      })
      setOptions(prev => ({ ...prev, docCode: [], docVersion: [] }))
    }
    if (level === 3) {
      dispatch(setFormFields({ formData: { docVersion: { value: '', label: '' } } }))
      setOptions(prev => ({ ...prev, docVersion: [] }))
    }
  }

  const fetchDocSectionOptions = () => {
    clearOptions(1)
    setOptions(prev => ({ ...prev, docSection: data?.data }))
  }

  const fetchDocCodeOptions = async args => {
    clearOptions(2)
    const { isSuccess: onSuccess, data } = await getDocumentOptions(args)
    if (onSuccess) setOptions(prev => ({ ...prev, docCode: data }))
  }

  const fetchDocVersionOptions = async args => {
    clearOptions(3)
    const { isSuccess: onSuccess, data } = await getDocumentOptions(args)
    if (onSuccess) setOptions(prev => ({ ...prev, docVersion: data }))
  }

  const handleChange = changedField => {
    const fieldValue = Object.values(changedField)[0]
    if (fieldValue instanceof Date && isValid(fieldValue)) {
      changedField = {
        [Object.keys(changedField)[0]]: fieldValue.toISOString(),
      }
    }
    if (Object.keys(changedField)?.[0] === 'docSection' && !!changedField?.docSection?.value)
      fetchDocCodeOptions({
        endPointSlug: 'form/fetchDocCode',
        payload: { docSection: changedField?.docSection?.value, entityCode: navData?.[NavDataValue.ENTITY_CODE] },
      })
    if (Object.keys(changedField)?.[0] === 'docCode' && !!changedField?.docCode?.value)
      fetchDocVersionOptions({
        endPointSlug: 'form/fetchDocVersion',
        payload: { docCode: changedField?.docCode?.value, entityCode: navData?.[NavDataValue.ENTITY_CODE] },
      })
    dispatch(setFormFields({ formData: changedField }))
  }

  return (
    <AppContainer className="container h-auto mx-0 mb-5 pb-5">
      <Form
        onChange={handleChange}
        submittable={true}
        onSubmit={() => alert('Form is going to be submitted')}
      >
        <div className="row">
          <div className="col-6">
            <FormSelect
              required
              label="Document Section"
              name="docSection"
              data={options.docSection}
              value={formData?.docSection}
            />
            <FormSelect
              required
              label="Document Code"
              name="docCode"
              data={options.docCode}
              value={formData?.docCode}
            />
            <FormSelect
              label="Document Version"
              name="docVersion"
              data={options.docVersion}
              value={formData?.docVersion}
              className="col-12"
            />
            <FormSelect
              required
              label="Document Status"
              name="docStatus"
              data={options.docStatus}
              value={formData?.docStatus}
              className="col-12"
            />
            <FormDateSelector
              name="documentDueDate"
              value={stringToDate(formData?.documentDueDate as string)}
              label="Document Due Date"
              className="col-12"
            />
            <FormRadioGroup
              inline
              label="Waive Request"
              data={waiveRequestData}
              name="waiveRequest"
              value={formData?.waiveRequest}
              className="col-12"
            />
            <FormRadioGroup
              inline
              label="Credit Use"
              data={creditUseData}
              name="creditUse"
              value={formData?.creditUse}
              className="col-12"
            />
            <FormDateSelector
              name="creditUseDate"
              value={stringToDate(formData?.creditUseDate as string)}
              label="Credit Use Date"
              className="col-12"
            />
            <FormDateSelector
              name="creditApprovalDate"
              value={stringToDate(formData?.creditApprovalDate as string)}
              label="Credit Approval Date"
              className="col-12"
            />
          </div>
          <div className="col-6">
            <FormSelect
              required
              data={options.trackingStatus}
              value={formData?.trackingStatus}
              name="trackingStatus"
              label="Tracking Status"
              className="col-12"
            />
            <FormSelect
              data={options.physicalStatus}
              value={formData?.physicalStatus}
              name="physicalStatus"
              label="Physical Status"
              className="col-12"
            />
            <FormSelect
              data={options.processStatus}
              value={formData?.processStatus}
              name="processStatus"
              label="Process Status"
              className="col-12"
            />
          </div>
        </div>
      </Form>
    </AppContainer>
  )
}

export default FormBodyRenderer
