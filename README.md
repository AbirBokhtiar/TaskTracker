
# Task Tracker in Google Sheets

## Overview
This Task Tracker helps you manage and track tasks in Google Sheets. With auto-generated Task IDs, automated status updates, and formulas to calculate task completion, this sheet is an effective tool for organizing your work. It also includes dropdowns for easy data input, conditional formatting for task prioritization, and email reminders for overdue tasks.

---

## Table of Contents
1. [Google Sheets Setup](#1-google-sheets-setup)
2. [Essential Formulas](#2-essential-formulas)
3. [Conditional Formatting](#3-conditional-formatting)
4. [Dropdown Menus](#4-dropdown-menus)
5. [Google Apps Script (Optional)](#5-google-apps-script-optional)
6. [Filters and Sorting](#6-filters-and-sorting)
7. [How to Set Up and Use the Task Tracker](#7-how-to-set-up-and-use-the-task-tracker)
8. [Additional Customizations](#8-additional-customizations)

---

## 1. Google Sheets Setup

Set up your Google Sheets with the following columns to track your tasks:

| **Column**   | **Description**                                           |
|--------------|-----------------------------------------------------------|
| **Task ID**  | Auto-generated unique identifier for each task.           |
| **Task Name**| Name or description of the task.                          |
| **Assigned To**| Person responsible for the task.                        |
| **Due Date** | Date the task is due.                                     |
| **Priority** | Task's priority level (High, Medium, Low).                |
| **Status**   | Task's current status (To-Do, In Progress, Completed).    |
| **Progress** | Completion percentage of the task (0-100%).               |
| **Comments** | Additional notes or remarks.                              |

---

## 2. Essential Formulas

### Auto-Generate Task ID (Column A)
Use the following formula in **Cell A2** to auto-generate Task IDs:

```excel
=IF(B2<>"", ROW()-1, "")
```

### Auto-Update Task Status (Column G)
Use the following formula in **Cell G2** to update the task status based on the progress:

```excel
=IF(F2=100, "Completed", IF(F2>=50, "In Progress", "To-Do"))
```

### Track Overall Progress (Cell F101)
To calculate the average task progress:

```excel
=AVERAGE(F2:F100)
```

### Count Tasks by Status:
Count tasks in each status using these formulas:

- **Completed Tasks**: 
  ```excel
  =COUNTIF(G2:G100, "Completed")
  ```

- **In Progress Tasks**: 
  ```excel
  =COUNTIF(G2:G100, "In Progress")
  ```

- **To-Do Tasks**: 
  ```excel
  =COUNTIF(G2:G100, "To-Do")
  ```

---

## 3. Conditional Formatting

### Highlight Tasks by Priority:
- Select **Column E** (Priority).
- Go to **Format > Conditional Formatting**.
- Set the rule for when **Text contains** `High` and pick a color (e.g., Red) to highlight **High Priority** tasks.

### Highlight Completed Tasks:
- Select **Column G** (Status).
- Set the rule for when the status is **Completed** and choose a color (e.g., Green).

---

## 4. Dropdown Menus

### Priority Dropdown:
1. Select **Column E** (Priority).
2. Go to **Data > Data Validation**.
3. Under **Criteria**, select **List of items** and enter `High, Medium, Low`.
4. Click **Done**.

### Status Dropdown:
1. Select **Column G** (Status).
2. Go to **Data > Data Validation**.
3. Under **Criteria**, select **List of items** and enter `To-Do, In Progress, Completed`.
4. Click **Done**.

---

## 5. Google Apps Script (Optional)

You can set up automated email reminders for overdue tasks using Google Apps Script. Here’s a sample script:

```javascript
function sendDueDateReminders() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("Sheet1");
  var data = sheet.getDataRange().getValues();
  
  var today = new Date();
  
  for (var i = 1; i < data.length; i++) {
    var dueDate = new Date(data[i][3]);
    var email = data[i][2];
    
    if (dueDate < today && data[i][6] !== "Completed") {
      var subject = "Task Reminder: " + data[i][1];
      var body = "Dear " + data[i][2] + ",

This is a reminder that your task "" + data[i][1] + "" is overdue. Please update the task status.

Best Regards,
Task Tracker";
      MailApp.sendEmail(email, subject, body);
    }
  }
}
```

1. Go to **Extensions > Apps Script**.
2. Paste the script into the editor and save.
3. Set a trigger to run the script daily.

---

## 6. Filters and Sorting

You can use **Filters** to sort and view tasks by **Priority**, **Status**, or **Due Date**:
1. Click on the filter icon in the header row.
2. Choose filter criteria (e.g., **High Priority** or **Completed** tasks).
3. This allows you to quickly manage and review your tasks.

---

## 7. How to Set Up and Use the Task Tracker

1. **Create Your Sheet**:
   - Open a new Google Sheets file and set up columns and formulas as described.
2. **Input Task Data**:
   - Enter tasks with details such as **Task Name**, **Assigned To**, **Due Date**, and **Priority**.
   - The **Task ID** will auto-generate.
   - Update **Progress** as the task progresses, and **Status** will update automatically.
3. **Monitor Progress**:
   - Use the **Completion Rate** formula to track overall progress.
   - Use the **Count by Status** formulas to see how many tasks are in each stage.
4. **Set Up Email Reminders**:
   - Use **Google Apps Script** to send automated email reminders for overdue tasks.

---

## 8. Additional Customizations

You can extend the functionality of your Task Tracker by:
- Adding a **Gantt Chart** for visual progress tracking.
- Using **Google Sheets Add-ons** for advanced project management.
- Creating a **Kanban Board** using Google Sheets’ **Cell Color Coding** and **Charts**.

---

This simple but powerful Task Tracker will help you manage and track tasks, monitor progress, and automate reminders. Feel free to customize it to fit your project’s needs!
