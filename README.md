

import React, { useState } from 'react';

const data = [
  { name: 'John', age: 25, job: 'developer' },
  { name: 'Jane', age: 32, job: 'designer' },
  { name: 'Bob', age: 28, job: 'developer' },
  { name: 'Sara', age: 22, job: 'manager' },
];

const MultiFilter = () => {
  const [filters, setFilters] = useState({ name: '', age: '', job: '' });

  const handleFilterChange = (event) => {
    const { name, value } = event.target;
    setFilters({ ...filters, [name]: value });
  };

  const filteredData = data.filter(item =>
    Object.entries(filters).every(([key, value]) =>
      !value || item[key].toLowerCase().includes(value.toLowerCase())
    )
  );

  return (
    <div>
      <form>
        <label>
          Name:
          <input type="text" name="name" onChange={handleFilterChange} />
        </label>
        <label>
          Age:
          <input type="text" name="age" onChange={handleFilterChange} />
        </label>
        <label>
          Job:
          <input type="text" name="job" onChange={handleFilterChange} />
        </label>
      </form>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Age</th>
            <th>Job</th>
          </tr>
        </thead>
        <tbody>
          {filteredData.map(item => (
            <tr key={item.name}>
              <td>{item.name}</td>
              <td>{item.age}</td>
              <td>{item.job}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default MultiFilter;

