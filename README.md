import React, { useState } from 'react';

const TaskTracker = () => {
    const [tasks, setTasks] = useState([]);
    const [newTask, setNewTask] = useState({ 
        title: '', 
        description: '', 
        startDate: new Date().toISOString().split('T')[0], // Default to current date
        endDate: '', 
        status: 'Pending', 
        assignee: '', 
        priority: 'P2' 
    });

    // Function to handle form submission
    const handleSubmit = (e) => {
        e.preventDefault();
        // Add the new task to the tasks array
        setTasks([...tasks, newTask]);
        // Reset the form fields
        setNewTask({ 
            title: '', 
            description: '', 
            startDate: new Date().toISOString().split('T')[0], 
            endDate: '', 
            status: 'Pending', 
            assignee: '', 
            priority: 'P2' 
        });
    };

    // Function to handle changes in the form fields
    const handleChange = (e) => {
        const { name, value } = e.target;
        // Update the newTask state with the changed field
        setNewTask({ ...newTask, [name]: value });
    };

    // Function to handle task deletion
    const handleDelete = (index) => {
        const updatedTasks = [...tasks];
        updatedTasks.splice(index, 1);
        setTasks(updatedTasks);
    };

    // Combined CSS styles using tagged template literals
    const taskTrackerStyles = `
        .task-tracker {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f9f9f9;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
            font-family: Arial, sans-serif;
            color: #333;
        }

        .task-tracker h2 {
            font-size: 24px;
            margin-bottom: 20px;
            color: #007bff;
        }

        .task-tracker form {
            display: flex;
            flex-direction: column;
        }

        .task-tracker input[type="text"],
        .task-tracker input[type="date"],
        .task-tracker select,
        .task-tracker button {
            margin-bottom: 10px;
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
        }

        .task-tracker input[type="text"]:focus,
        .task-tracker input[type="date"]:focus,
        .task-tracker select:focus,
        .task-tracker button:focus {
            outline: none;
            border-color: #007bff;
            box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
        }

        .task-tracker button {
            background-color: #007bff;
            color: #fff;
            border: none;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .task-tracker button:hover {
            background-color: #0056b3;
        }

        .task-list {
            margin-top: 20px;
        }

        .task-list h3 {
            font-size: 20px;
            margin-bottom: 10px;
            color: #007bff;
        }

        .task-list ul {
            list-style-type: none;
            padding: 0;
        }

        .task-list li {
            margin-bottom: 8px;
            background-color: #fff;
            padding: 10px;
            border-radius: 4px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        }

        .task-list li strong {
            color: #007bff;
        }
    `;

    return (
        <div className="task-tracker">
            {/* Inject CSS styles */}
            <style>{taskTrackerStyles}</style>
            <h2>SIMPLE TASK TRACKER</h2>
            <form onSubmit={handleSubmit}>
                <input type="text" name="title" placeholder="Title" value={newTask.title} onChange={handleChange} />
                <input type="text" name="description" placeholder="Description" value={newTask.description} onChange={handleChange} />
                <input type="date" name="startDate" value={newTask.startDate} onChange={handleChange} />
                <input type="date" name="endDate" value={newTask.endDate} onChange={handleChange} />
                <select name="status" value={newTask.status} onChange={handleChange}>
                    <option value="Pending">Pending</option>
                    <option value="In Progress">In Progress</option>
                    <option value="Completed">Completed</option>
                    <option value="Deployed">Deployed</option>
                    <option value="Deferred">Deferred</option>
                </select>
                <input type="text" name="assignee" placeholder="Assignee" value={newTask.assignee} onChange={handleChange} />
                <select name="priority" value={newTask.priority} onChange={handleChange}>
                    <option value="P0">P0</option>
                    <option value="P1">P1</option>
                    <option value="P2">P2</option>
                </select>
                <button type="submit">Add Task</button>
            </form>
            <div className="task-list">
                <h3>Tasks Displays</h3>
                <ul>
                    {tasks.map((task, index) => (
                        <li key={index}>
                            <strong>Title:</strong> {task.title}<br />
                            <strong>Description:</strong> {task.description} <br />
                            <strong>Start Date:</strong> {task.startDate} <br />
                            <strong>End Date:</strong> {task.endDate} <br />
                            <strong>Status:</strong> {task.status}<br />
                            <strong>Assignee:</strong> {task.assignee}<br />
                            <strong>Priority:</strong> {task.priority}<br /><br />
                            <button onClick={() => handleDelete(index)}>Delete</button>
                        </li>
                    ))}
                </ul>
            </div>
        </div>
    );
};

export default TaskTracker;

