import React, { useState } from 'react';

const Dropdowns = () => {
  // Sample data for options
  const grandparents = [
    { id: 1, name: "Grandparent 1" },
    { id: 2, name: "Grandparent 2" },
    { id: 3, name: "Grandparent 3" }
  ];

  const parents = [
    { id: 1, name: "Parent 1", grandparentId: 1 },
    { id: 2, name: "Parent 2", grandparentId: 1 },
    { id: 3, name: "Parent 3", grandparentId: 2 },
    { id: 4, name: "Parent 4", grandparentId: 2 },
    { id: 5, name: "Parent 5", grandparentId: 3 }
  ];

  const children = [
    { id: 1, name: "Child 1", parentId: 1 },
    { id: 2, name: "Child 2", parentId: 1 },
    { id: 3, name: "Child 3", parentId: 2 },
    { id: 4, name: "Child 4", parentId: 3 },
    { id: 5, name: "Child 5", parentId: 4 },
    { id: 6, name: "Child 6", parentId: 5 }
  ];

  const [selectedGrandparent, setSelectedGrandparent] = useState(null);
  const [selectedParent, setSelectedParent] = useState(null);
  const [selectedChild, setSelectedChild] = useState(null);

  const handleGrandparentChange = (e) => {
    setSelectedGrandparent(parseInt(e.target.value));
    setSelectedParent(null);
    setSelectedChild(null);
  };

  const handleParentChange = (e) => {
    setSelectedParent(parseInt(e.target.value));
    setSelectedChild(null);
  };

  const handleChildChange = (e) => {
    setSelectedChild(parseInt(e.target.value));
  };

  return (
    <div>
      <label htmlFor="grandparent">Grandparent:</label>
      <select id="grandparent" onChange={handleGrandparentChange} value={selectedGrandparent || ''}>
        <option value="">Select Grandparent</option>
        {grandparents.map(grandparent => (
          <option key={grandparent.id} value={grandparent.id}>{grandparent.name}</option>
        ))}
      </select>

      <label htmlFor="parent">Parent:</label>
      <select id="parent" onChange={handleParentChange} value={selectedParent || ''} disabled={!selectedGrandparent}>
        <option value="">Select Parent</option>
        {parents.map(parent => {
          if (parent.grandparentId === selectedGrandparent) {
            return <option key={parent.id} value={parent.id}>{parent.name}</option>;
          } else {
            return null;
          }
        })}
      </select>

      <label htmlFor="child">Child:</label>
      <select id="child" onChange={handleChildChange} value={selectedChild || ''} disabled={!selectedParent}>
        <option value="">Select Child</option>
        {children.map(child => {
          if (child.parentId === selectedParent) {
            return <option key={child.id} value={child.id}>{child.name}</option>;
          } else {
            return null;
          }
        })}
      </select>
    </div>
  );
};

export default Dropdowns;
