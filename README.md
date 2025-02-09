import React from 'react';
import { Card, CardHeader, CardTitle, CardContent } from '@/components/ui/card';
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer } from 'recharts';

const FinancialAnalysis = () => {
  // ข้อมูลงบการเงิน SCB ปี 2561-2565 (หน่วย: ล้านบาท)
  const financialData = [
    {
      year: '2561',
      totalAssets: 3187345,
      revenue: 141341,
      costOfSales: 28268,
      netProfit: 40068,
    },
    {
      year: '2562',
      totalAssets: 3228725,
      revenue: 144809,
      costOfSales: 29871,
      netProfit: 40436,
    },
    {
      year: '2563',
      totalAssets: 3280442,
      revenue: 134346,
      costOfSales: 27803,
      netProfit: 27218,
    },
    {
      year: '2564',
      totalAssets: 3301768,
      revenue: 122255,
      costOfSales: 25673,
      netProfit: 35599,
    },
    {
      year: '2565',
      totalAssets: 3454841,
      revenue: 138492,
      costOfSales: 29083,
      netProfit: 37491,
    }
  ];

  // คำนวณอัตราส่วนทางการเงิน
  const ratios = financialData.map(data => ({
    year: data.year,
    ROA: ((data.netProfit / data.totalAssets) * 100).toFixed(2),
    NPM: ((data.netProfit / data.revenue) * 100).toFixed(2),
    costToRevenue: ((data.costOfSales / data.revenue) * 100).toFixed(2)
  }));

  return (
    <div className="space-y-6">
      <Card>
        <CardHeader>
          <CardTitle>อัตราส่วนทางการเงินที่สำคัญ SCB (2561-2565)</CardTitle>
        </CardHeader>
        <CardContent>
          <div className="h-80">
            <ResponsiveContainer width="100%" height="100%">
              <LineChart data={ratios}>
                <CartesianGrid strokeDasharray="3 3" />
                <XAxis dataKey="year" />
                <YAxis />
                <Tooltip />
                <Legend />
                <Line type="monotone" dataKey="ROA" name="ROA (%)" stroke="#8884d8" />
                <Line type="monotone" dataKey="NPM" name="Net Profit Margin (%)" stroke="#82ca9d" />
                <Line type="monotone" dataKey="costToRevenue" name="Cost to Revenue (%)" stroke="#ffc658" />
              </LineChart>
            </ResponsiveContainer>
          </div>
        </CardContent>
      </Card>

      <Card>
        <CardHeader>
          <CardTitle>แนวโน้มผลการดำเนินงาน SCB (2561-2565)</CardTitle>
        </CardHeader>
        <CardContent>
          <div className="h-80">
            <ResponsiveContainer width="100%" height="100%">
              <LineChart data={financialData}>
                <CartesianGrid strokeDasharray="3 3" />
                <XAxis dataKey="year" />
                <YAxis />
                <Tooltip />
                <Legend />
                <Line type="monotone" dataKey="totalAssets" name="สินทรัพย์รวม (ล้านบาท)" stroke="#8884d8" />
                <Line type="monotone" dataKey="revenue" name="รายได้รวม (ล้านบาท)" stroke="#82ca9d" />
                <Line type="monotone" dataKey="netProfit" name="กำไรสุทธิ (ล้านบาท)" stroke="#ffc658" />
              </LineChart>
            </ResponsiveContainer>
          </div>
        </CardContent>
      </Card>
    </div>
  );
};

export default FinancialAnalysis;
