import React from 'react'
import { useEffect, useState } from 'react'
// import { useAppSelector} from '~components/statemanagement/hooks'
import './customform.scss'
import {
  AppContainer,
  FormSelect,
  Form,
  FormDateSelector,
  FormRadioGroup,
  FormDateTimePicker,
  FormCreatableSelect,
} from '@connectcore/connect-components-react'
import mockData1 from './mockData.js'
import mockData2 from './mockdata2.js'
import mockData3 from './mockData3.js'

const FormBodyRenderer = () => {
  const [firstOptions, setFirstOptions] = useState([mockData1?.data]);
  const [secondOptions, setSecondOptions] = useState([]);
  const [thirdOptions, setThirdOptions] = useState([]);

  const [selectedFirst, setSelectedFirst] = useState<string>('');
  const [selectedSecond, setSelectedSecond] = useState('');
  const [selectedThird, setSelectedThird] = useState('');

  const booleanEntry = [
    { value: 'yes', text: 'Yes' },
    { value: 'no', text: 'No' },
  ]
  useEffect(() => {
    // Fetch first dropdown data
    fetchFirstOptions();
  }, []);

  const clearOptions = (value?:number) => {
    switch (value) {
      case 2:
        setSelectedSecond('');
        break;
      case 3:
        setSelectedThird('');
        break;
      default:
        setSelectedSecond('');
        setSelectedThird('');
        break;
    }


  }

  const fetchFirstOptions = async () => {
    clearOptions();
    // Mock API call or actual API call
    //  const response = await fetch('mockData.json');
    // const data = await response.json();
    setFirstOptions(mockData1?.data);
  };

  const fetchSecondOptions = async () => {
    clearOptions(3);
    // Make API call based on selected value from first dropdown
    // Example: fetch(`/api/second-dropdown?firstValue=${selectedFirst}`)

    setSecondOptions(mockData2?.data);
  };

  const fetchThirdOptions = async () => {
    // Make API call based on selected value from second dropdown
    // Example: fetch(`/api/third-dropdown?secondValue=${selectedSecond}`)
    setThirdOptions(mockData3?.data);
  };

  const handleFirstChange = (e) => {
    setSelectedFirst(e?.value);
    fetchSecondOptions();
  };

  const handleSecondChange = (e) => {
    setSelectedSecond(e?.value);
    fetchThirdOptions();
  };

  const handleThirdChange = (e) => {
    setSelectedThird(e?.value);
  };


  return (
    <>
      <AppContainer className="container h-auto mx-0 mb-5 pb-5">
        <Form >
          <div className="row">
            <div className="col-6">
              <FormCreatableSelect
                label="Document Section"
                data={firstOptions}
                value={selectedFirst}
                onChange={handleFirstChange}
              />
              <FormCreatableSelect
                label="Document Code"
                data={secondOptions}
                value={selectedSecond}
                onChange={handleSecondChange}
              />
              <FormCreatableSelect
                label="Document Version"
                data={thirdOptions}
                value={selectedThird}
                onChange={handleThirdChange}
              />

              <FormSelect required name="formSelect" label="Document Code" className="col-12" />
              <FormSelect required name="formSelect" label="Document Version" className="col-12" />
              <FormSelect required name="formSelect" label="Document Status" className="col-12" />

              <FormDateTimePicker
                required
                name="someDate"
                initialValue={new Date()}
                label="Document Due Date"
                className="col-12"
              />
              <FormRadioGroup
                label="Waive Request"
                data={booleanEntry}
                name="formBasicUsageExample"
                required
                className="col-12"
              />
              <FormRadioGroup
                label="Credit Use"
                data={booleanEntry}
                name="formBasicUsageExample"
                required
                className="col-6"
              />
              <FormDateSelector
                required
                name="someDate"
                initialValue={new Date()}
                label="Credit Use Date"
                className="col-12"
              />
              <FormDateSelector
                required
                name="someDate"
                initialValue={new Date()}
                label="Credit Approval Date"
                className="col-12"
              />
            </div>
            <div className="col-6">
              <FormSelect required name="formSelect" label="Tracking Status" className="col-12" />
              <FormSelect required name="formSelect" label="Physical Status" className="col-12" />
              <FormSelect required name="formSelect" label="Process Status" className="col-12" />
            </div>
          </div>
        </Form>
      </AppContainer>
    </>
  )
}

// const Form = props => {
//   // const dispatch = useAppDispatch()

//   useEffect(()=>{
//     renderForm()
//   },[props.isEditMode,(props.bodySchema?.components ?? []).length,props?.formData])

//   const asyncRender = async () => {
//    console.log('we have to come back here')
//   }

//   const renderForm = () => asyncRender().catch(e=>console.error(e))

//   return (
//     <div id = 'form-body-renderer'/>
//   )
// }

// const FormAbsent = () => {
//   return (
//     <EmptyState
//       style={{ height: '100%', width: '100%', margin: 'auto' }}
//       show
//       icon="info"
//       iconSize="lg"
//       text="No Form Found To Load"
//     />
//   )
// }

export default React.memo(FormBodyRenderer)
