import React, { useState } from "react";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from "recharts";

export default function ChartFormBuilder() {
  const [jsonData, setJsonData] = useState("[{\"name\":\"A\",\"value\":10},{\"name\":\"B\",\"value\":20}]");
  const [data, setData] = useState(JSON.parse(jsonData));
  
  const handleInputChange = (e) => {
    setJsonData(e.target.value);
  };

  const handleUpdateChart = () => {
    try {
      const parsedData = JSON.parse(jsonData);
      setData(parsedData);
    } catch (error) {
      alert("Invalid JSON format");
    }
  };

  return (
    <div className="p-4 max-w-2xl mx-auto">
      <Card>
        <CardContent className="p-4 space-y-4">
          <Input
            type="text"
            value={jsonData}
            onChange={handleInputChange}
            placeholder='Enter JSON data (e.g., [{"name":"A","value":10}])'
          />
          <Button onClick={handleUpdateChart}>Update Chart</Button>
        </CardContent>
      </Card>
      <div className="mt-6">
        <ResponsiveContainer width="100%" height={300}>
          <LineChart data={data}>
            <CartesianGrid strokeDasharray="3 3" />
            <XAxis dataKey="name" />
            <YAxis />
            <Tooltip />
            <Line type="monotone" dataKey="value" stroke="#8884d8" strokeWidth={2} />
          </LineChart>
        </ResponsiveContainer>
      </div>
    </div>
  );
}
