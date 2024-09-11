# blockchain-task

//SPDX-License-Identifier: MIT
pragma solidity  ^0.8.0;

contract todolist{
    struct task{
        string description;
        bool iscompleted;
        uint priority; //1-for high priority,2-for medium priority,3-Low priority
        uint duedate;
        string category;
    }

    mapping(address => task[]) private userTasks;

    function addtask(string memory _description , uint _priority, uint _duedate, string memory _category)public{
        userTasks[msg.sender].push(task(_description, false, _priority, _duedate, _category));
    }     // this above code will be used for creating a new task

    function markTaskCompleted(uint _taskIndex) public {
        require(_taskIndex < userTasks[msg.sender].length, "Invalid task index");
        userTasks[msg.sender][_taskIndex].iscompleted = true;
    }   //this above code will be used for marking task as completed

    function removeTask(uint _taskIndex) public {
        require(_taskIndex < userTasks[msg.sender].length, "Invalid task index");
        for (uint i = _taskIndex; i < userTasks[msg.sender].length - 1; i++) {
            userTasks[msg.sender][i] = userTasks[msg.sender][i + 1];
        }
        userTasks[msg.sender].pop();
    }  //this above code will be used to remove a task

    function editTask(uint _taskIndex, string memory _newDescription) public {
        require(_taskIndex < userTasks[msg.sender].length, "Invalid task index");
        userTasks[msg.sender][_taskIndex].description = _newDescription;
    } // this above task will be used to edit the tasks

}
