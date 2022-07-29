import React, { useState } from "react";
import machineList from "./machineList.json";

function SelectMachine() {
  const [machineName, setMachineName] = useState("");
  const [machineType, setMachineType] = useState("");
  const [machineCount, setMachineCount] = useState("");

  const [id, setId] = useState("");
  const [message, setMessage] = useState("");

  function displayMessage() {
    machineList.forEach((machine) => {
      if (machine.machineType == machineType) {
        if (machineCount > machine.availableMachines) {
          setId("failure");
          setMessage(`Sorry only ${machine.availableMachines} are available`);
        } else {
          setId("success");
          setMessage(`${machineCount} machines approved for your team.`);
          machine.availableMachines=machine.availableMachines-machineCount;
        }
      }
    });
  }

  return (
    <div>
      <header>Select Your Machine</header>
      {console.log(machineList)}
      <table>
        <thead>
          <th>Machine Type</th>
          <th>Processor</th>
          <th>Platform</th>
          <th>Primary Memory</th>
        </thead>

        {machineList.map((machine) => {
          return (
            <tr key={machine.machineId}>
              <td id={`machineType${machine.machineId}`}>
                {machine.machineType}
              </td>
              <td id={`processor${machine.machineId}`}>{machine.processor}</td>
              <td id={`platform${machine.machineId}`}>{machine.platform}</td>
              <td id={`primaryMemory${machine.machineId}`}>
                {machine.primaryMemory}
              </td>
            </tr>
          );
        })}
      </table>

      <div>
        <p>Give your team name,machine type and count</p>
        Team Name{" "}
        <input
          type="text"
          id="teamName"
          onChange={(e) => setMachineName(e.target.value)}
        ></input>
        Machine Type{" "}
        <input
          type="text"
          id="machineType"
          onChange={(e) => setMachineType(e.target.value)}
        ></input>
        Machine Count{" "}
        <input
          type="number"
          id="machineCount"
          onChange={(e) => setMachineCount(e.target.value)}
        ></input>
        <button id="submit" onClick={displayMessage}>
          Submit
        </button>

        {
            id!=""?<p id={id}>{message}</p>:""
        }
      </div>
    </div>
  );
}

export default SelectMachine;
