A company wants to implement a smart contract that facilitates weekly wage payments to its employees. The company wants to automate the payment process, so the employees receive their wages each week without requiring manual intervention. The contract needs to be secure, transparent, and auditable.

The company needs to be able to add funds to the contract and specify the amount to be paid to each employee each week. The contract should maintain a record of all payments made to each employee and ensure that no employee can be paid more than their designated weekly amount. In addition, the contract should allow employees to withdraw their wages at any time.

The contract should be designed in such a way that it can handle a large number of employees and payments without any performance issues. The contract should also be flexible enough to allow the company to add or remove employees and adjust the payment amounts as needed.

Overall, the company wants a smart contract that can automate the wage payment process, increase transparency, and reduce the risk of errors or fraud.
```
Constraints:

  Only the employer should be able to pay employees.

Hints
  Set the contract creator as the owner in the constructor.
  Update the addFunds() function to update the totalFunds variable with the amount of ether added.
```

### Solution

```
contract Payroll {
    address public employer;
    mapping(address => uint) public employeeSalaries;
    uint public totalFunds;

    constructor() {
        // TODO
        employer = msg.sender;
    }

    function addFunds() public payable {
        // TODO
        require(msg.sender == employer, "Only Employer can add funds");
        totalFunds += msg.value;
    }

    function getTotalFunds() public view returns (uint) {
        // TODO
        return totalFunds;
    }

    function payEmployee(address employee) public {
        // TODO
        uint salary = employeeSalaries[employee];
        require(totalFunds >= salary, "Not enough funds to pay employee.");
        (bool sent, ) = employee.call{value: salary}("");
        require(sent, "Failed to send Ether to the employee.");
      
    }

    function setEmployeeSalary(address employee, uint salary) public {
        // TODO
        require(msg.sender == employer, "Only the employer can set employee salary.");
        employeeSalaries[employee] = salary;
    }
}
```
