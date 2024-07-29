addTaskButtonClicked(task: Task = new Task()): void {
    const MAX_TASKS = 20; // Define the maximum number of tasks
    const teamList = this._resource.getContextValue('teamMap');
    this.teamName = teamList[this.checklistEdit.teamCode];
    
    // Check the number of existing tasks
    if (this.checklistEdit.tasks.length >= MAX_TASKS) {
        // Optional: Log or alert the user that the limit has been reached
        console.warn('Task limit reached. Cannot add more tasks.');
        return; // Exit the function to prevent adding more tasks
    }

    if (this.checklistEdit.workflowId === 0) {
        this.favMetrics.logMetric(
            'Workflow Manager Create Checklist',
            'Add New Task',
            {'Team Name': this.teamName}
        );
    } else {
        this.favMetrics.logMetric(
            'Workflow Manager Create Checklist',
            'Add New Task',
            {'Workflow ID': this.checklistEdit.workflowId, 'Team Name': this.teamName}
        );
    }

    this.createNewTask();
}
