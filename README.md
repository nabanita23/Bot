import React, { useState, useEffect } from 'react';
import axios from 'axios';

function CascadingDropdown() {
    const [options1, setOptions1] = useState([]);
    const [selectedOption1, setSelectedOption1] = useState('');
    const [options2, setOptions2] = useState([]);
    const [selectedOption2, setSelectedOption2] = useState('');
    const [options3, setOptions3] = useState([]);
    const [selectedOption3, setSelectedOption3] = useState('');

    useEffect(() => {
        // Fetch data for the first dropdown
        axios.get('api/endpoint1')
            .then(response => {
                setOptions1(response.data);
            })
            .catch(error => {
                console.error('Error fetching data for dropdown 1:', error);
            });
    }, []);

    useEffect(() => {
        if (selectedOption1 !== '') {
            // Fetch data for the second dropdown based on the selected value of the first dropdown
            axios.get(`api/endpoint2?param=${selectedOption1}`)
                .then(response => {
                    setOptions2(response.data);
                })
                .catch(error => {
                    console.error('Error fetching data for dropdown 2:', error);
                });
        }
    }, [selectedOption1]);

    useEffect(() => {
        if (selectedOption2 !== '') {
            // Fetch data for the third dropdown based on the selected value of the second dropdown
            axios.get(`api/endpoint3?param=${selectedOption2}`)
                .then(response => {
                    setOptions3(response.data);
                })
                .catch(error => {
                    console.error('Error fetching data for dropdown 3:', error);
                });
        }
    }, [selectedOption2]);

    const handleOption1Change = (event) => {
        setSelectedOption1(event.target.value);
        setSelectedOption2(''); // Reset second dropdown when the first dropdown changes
        setSelectedOption3(''); // Reset third dropdown when the first dropdown changes
    };

    const handleOption2Change = (event) => {
        setSelectedOption2(event.target.value);
        setSelectedOption3(''); // Reset third dropdown when the second dropdown changes
    };

    const handleOption3Change = (event) => {
        setSelectedOption3(event.target.value);
    };

    return (
        <div>
            <select value={selectedOption1} onChange={handleOption1Change}>
                <option value="">Select Option 1</option>
                {options1.map(option => (
                    <option key={option.id} value={option.value}>{option.label}</option>
                ))}
            </select>
            <select value={selectedOption2} onChange={handleOption2Change}>
                <option value="">Select Option 2</option>
                {options2.map(option => (
                    <option key={option.id} value={option.value}>{option.label}</option>
                ))}
            </select>
            <select value={selectedOption3} onChange={handleOption3Change}>
                <option value="">Select Option 3</option>
                {options3.map(option => (
                    <option key={option.id} value={option.value}>{option.label}</option>
                ))}
            </select>
        </div>
    );
}

export default CascadingDropdown;

