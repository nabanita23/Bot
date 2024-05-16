import React, { useEffect, useState } from 'react';
import './customform.scss';
import {
  AppContainer,
  FormSelect,
  Form,
  FormDateSelector,
  FormRadioGroup,
  FormDateTimePicker,
  FormCreatableSelect,
} from '@connectcore/connect-components-react';
import mockData1 from './mockData.js';
import mockData2 from './mockData2.js';
import mockData3 from './mockData3.js';

const FormBodyRenderer = () => {
  const [options, setOptions] = useState({
    first: mockData1?.data,
    second: [],
    third: [],
  });

  const [selected, setSelected] = useState({
    first: '',
    second: '',
    third: '',
  });

  const booleanEntry = [
    { value: 'yes', text: 'Yes' },
    { value: 'no', text: 'No' },
  ];

  useEffect(() => {
    fetchFirstOptions();
  }, []);

  const clearOptions = (level) => {
    if (level >= 2) setSelected(prev => ({ ...prev, second: '', third: '' }));
    if (level === 3) setSelected(prev => ({ ...prev, third: '' }));
  };

  const fetchFirstOptions = async () => {
    clearOptions(1);
    setOptions(prev => ({ ...prev, first: mockData1?.data }));
  };

  const fetchSecondOptions = async () => {
    clearOptions(2);
    // try {
    //   const response = await api.post(endpoint, data);
    //   console.log('Response:', response.data);
    //   return response.data;
    // } catch (error) {
    //   console.error('Error posting data:', error);
    //   throw error; // Re-throw error for further handling
    // }
    setOptions(prev => ({ ...prev, second: mockData2?.data }));
  };

  const fetchThirdOptions = async () => {
    setOptions(prev => ({ ...prev, third: mockData3?.data }));
  };

  const handleChange = (level, value) => {
    setSelected(prev => ({ ...prev, [level]: value }));
    if (level === 'first') fetchSecondOptions();
    if (level === 'second') fetchThirdOptions();
  };

  return (
    <AppContainer className="container h-auto mx-0 mb-5 pb-5">
      <Form>
        <div className="row">
          <div className="col-6">
            <FormCreatableSelect
              label="Document Section"
              data={options.first}
              value={selected.first}
              onChange={(e) => handleChange('first', e?.value)}
            />
            <FormCreatableSelect
              label="Document Code"
              data={options.second}
              value={selected.second}
              onChange={(e) => handleChange('second', e?.value)}
            />
            <FormCreatableSelect
              label="Document Version"
              data={options.third}
              value={selected.third}
              onChange={(e) => handleChange('third', e?.value)}
            />

            <FormSelect required name="documentCode" label="Document Code" className="col-12" />
            <FormSelect required name="documentVersion" label="Document Version" className="col-12" />
            <FormSelect required name="documentStatus" label="Document Status" className="col-12" />

            <FormDateTimePicker
              required
              name="dueDate"
              initialValue={new Date()}
              label="Document Due Date"
              className="col-12"
            />
            <FormRadioGroup
              label="Waive Request"
              data={booleanEntry}
              name="waiveRequest"
              required
              className="col-12"
            />
            <FormRadioGroup
              label="Credit Use"
              data={booleanEntry}
              name="creditUse"
              required
              className="col-6"
            />
            <FormDateSelector
              required
              name="creditUseDate"
              initialValue={new Date()}
              label="Credit Use Date"
              className="col-12"
            />
            <FormDateSelector
              required
              name="creditApprovalDate"
              initialValue={new Date()}
              label="Credit Approval Date"
              className="col-12"
            />
          </div>
          <div className="col-6">
            <FormSelect required name="trackingStatus" label="Tracking Status" className="col-12" />
            <FormSelect required name="physicalStatus" label="Physical Status" className="col-12" />
            <FormSelect required name="processStatus" label="Process Status" className="col-12" />
          </div>
        </div>
      </Form>
    </AppContainer>
  );
};

export default React.memo(FormBodyRenderer);
