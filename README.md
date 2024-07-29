  addTaskButtonClicked(task: Task = new Task()): void {
    const teamList = this._resource.getContextValue('teamMap');
    this.teamName = teamList[this.checklistEdit.teamCode];
    if (this.checklistEdit.workflowId === 0) {
      this.favMetrics.logMetric ('Workflow Manager Create Checklist', 'Add New Task', {'Team Name' : this.teamName});
    } else {
      this.favMetrics.logMetric ('Workflow Manager Create Checklist', 'Add New Task', {'Workflow ID' : this.checklistEdit.workflowId, 'Team Name' : this.teamName});
    }
    this.createNewTask();
  }
