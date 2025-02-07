# Municipal Services Application - We Got You

## Overview
The Municipal Services Application "We Got You" was created to make the process of reporting and handling requests for municipal services more efficient. Users can view local events and announcements, submit issues, track their status, and provide feedback. In addition to providing thorough explanations of the data structures utilized, with an emphasis on their function in the service request status feature, this document acts as a comprehensive guide for building, executing, and utilizing the program. 

---

## How to Compile and Run

### Prerequisites
- [.NET Framework](https://dotnet.microsoft.com/download/dotnet-framework) 
- Visual Studio (or any IDE supporting WPF and C# development).

### Compilation Instructions
1. Clone or download the project from the repository.
2. Open the project folder using Visual Studio.
3. Restore any required dependencies.
4. Build the solution:
   - Navigate to `Build > Build Solution` from the menu, or
   - Use the shortcut `Ctrl + Shift + B`.
  


---

## How to Use the Application

### Main Menu
![image](https://github.com/user-attachments/assets/41eed8a7-6f9d-4342-8ab0-55693ed3ea1c)
The main menu serves as the central hub for accessing various features:
- **Report Issues**: Navigate to a form where you can report municipal issues such as water leaks, potholes, etc.
- **Service request status**: Where the user can view the details of their reported issue including its status.
- **Events and Announcements**: View upcoming events, important announcements, and community updates.
- **Status request History**
- **Recommendations**







### Reporting Issues
![image](https://github.com/user-attachments/assets/4753c077-e05d-49bc-b39f-4bc642a8667e)

1. Click the "Report Issues" button from the Main Menu.
2. Fill out the required fields:
   - **Location**: Enter the location of the issue.
   - **Category**: Select a category (e.g., Environment, Infrastructure).
   - **Priority**: Specify the priority (e.g., High, Medium, Low).
   - **Description**: Provide a detailed description of the issue.
3. Attach relevant media files (e.g., photos of the issue) using the "Attach File" button.
4. Submit the form by clicking "Submit," which generates a unique `RequestId` for tracking.


### Viewing Service Request Status
![image](https://github.com/user-attachments/assets/b606494a-10b8-4be4-b882-fcc31d635b6f)

1. Navigate to the "Service Requests" section from the Main Menu.
2. Enter the `RequestId` to view the current status of your request.
3. The status, date of submission, and any updates will be displayed.


### Local Events and Announcements
![image](https://github.com/user-attachments/assets/2ca631a0-cce7-47a4-82d6-447c609f16e6)

1. Click the "Local Events and Announcements" button.
2. Browse upcoming events and announcements.
3. Use the filter button to sort events by category or date, or search for specific events using the search bar.


### Status Request History

![image](https://github.com/user-attachments/assets/88da6ca2-8cbc-4cda-975e-1ad978230613)

1. Click the Status request history" button on the Main Menu.
2. in the search bar, enter the Request ID (eg. 'SR001') to search for specificservice request.
3. the user can press the 'Back' button to return to the main menu. 
   
### Recommendations
![image](https://github.com/user-attachments/assets/c7b47dc2-c613-47db-b42c-63164fddc0fe)
in order for the user to view their recommendations, they must first search for an event in the Events and announcements window. 
The algorithm captures the first three letters of the searched phrase only if that phrase is entered more than 3 times as shown above.

![image](https://github.com/user-attachments/assets/8c09ebc4-cf91-43ba-ab91-95d3fa2faabf)

Once these condtions are met, the system can the provide the users recommendations.




---

## Explanation of Implemented Data Structures

### 1. **List**
#### Role and Contribution
- **Purpose**: Used to store collections of service requests and reported issues in sequential order.
- **Usage**: 
  - The list of issue reports is managed through `List<IssueReport>`.
  - The `List<ServiceRequest>` stores all service requests for tracking.
- **Efficiency**: `List` provides easy insertion and traversal capabilities, which are well-suited for storing data in the order of insertion.

#### Example:
```csharp
// Storing issue reports
List<IssueReport> reportedIssues = new List<IssueReport>();

// Adding a new report to the list
IssueReport report = new IssueReport
{
    Location = location,
    Category = category,
    Description = description,
    MediaAttachments = new List<string>(mediaAttachments),
    ReportedAt = DateTime.Now,
    RequestId = $"SR{reportedIssues.Count + 1:000}", // Unique ID generation
    Priority = priority
};

reportedIssues.Add(report);

### 2. **Dictionary**
#### Role and Contribution
- **Purpose**: Facilitates quick lookups, updates, and management of service requests using unique identifiers (`RequestId`).
- **Usage**: Maps `RequestId` keys to `ServiceRequest` objects for efficient querying.
- **Efficiency**: Provides average time complexity of `O(1)` for adding, retrieving, or updating items due to hash-based indexing.


```

### 3. **Queue**
#### Role and Contribution
- **Purpose**: Manages the processing order of pending service requests, ensuring a first-come, first-served system.
- **Usage**: New service requests are enqueued and processed in the order they are received.
- **Efficiency**: Provides constant-time enqueue and dequeue operations (`O(1)`), supporting fair request handling.

### 4. **Min Heap**
**Usage**: The heap is used to prioritize service requests based on urgency (priority levels: High, Medium, Low).
**Implementation**: A Priority Queue was implemented using a Min-Heap, ensuring that high-priority requests (e.g., "High") are processed before lower-priority ones (e.g., "Medium" and "Low").

![image](https://github.com/user-attachments/assets/0cc28028-7dd6-4a22-9d67-34e40417b389)

### 5. **Treeview**
**Usage**: The TreeView displays grouped statuses using the sorted data from StatusHeap.

## **Max heap**
- **Usage**: is in charge of using a max-heap structure to manage and prioritize service request statuses. It arranges statuses according to recency (more recent updates take precedence) and urgency (Critical being the highest priority). It offers ways to add, remove, and filter statuses. 





### 4. **SortedDictionary**
#### Role and Contribution
- **Purpose**: Maintains service requests in sorted order based on keys (e.g., request dates).
- **Usage**: Useful for scenarios where sorting based on request creation timestamps is needed. Also used for sotring Hardcoded data
- **Efficiency**: Provides `O(log n)` time complexity for insertion and lookup operations, offering a balance between speed and order preservation.

### 5. **basic Tree**
**usage**: stores parameters for a speficic request ID( ID, Status, Updated at, Updated by, date)



---





## Smart Recommendations and Local Events Feature(Updated)
The "Smart Recommendations" feature analyzes user search history and preferences using data structures like sets or custom algorithms to suggest relevant events.
this feature has been updated from the previous part- the Smart recommendations list accumulates rather than reseting after searching for different events. 

## Technical implementation of structures:
**Request Visualisation**
- GridView used for request listing
- Status-based Treeview representation
- Priority-based sorting techniques
- neat and user-friendly interface
- simple and efficient data visualization
- Responsive grid view accross the app.
- Visual feedback for each user interaction(loading bar, messages) 
- Filtering functionality

**Interface**
Search Functionality:
- uses multiple search criteria (ID, Description, Status, Priority, Location and date)
- Real-time search results

---

## Project file structure:
- MainWindow.xaml.cs and MainWindow.xaml: Main menu navigation
- ReportIssuesWindow.xaml.cs and .xaml: window for reporting issues
- LocalEventsWindow.xaml.cs and .xaml: Window for viewing all events
- ServiceRequestStausForm.xaml.cs and .xaml: Form for viewing details of service requests
- StatusHeap.cs: for managing and prioritizing service request statuses
- StatusHistoryTree.cs: tree used to store service request parameters
- StatusHistoryWindow.cs: the UI component that presents status history data
- FilterWindow.xaml.cs and .xaml: Window for filtering search results for the events/announcements

## More technical Information:
- Fronted designed with WPF(XAML). and backend designed with C#
- User interface has a consistent and pleasant colour scheme.
- backend contains numerous data structures such as heaps, trees, dictionaries


## Code Attribution
- Video Title: C# WPF UI | How to Design Input Form in WPF | Data Entry Form App
- Author: C# WPF UI Academy
- Published: 29 April 2022
- I used this video for inspiration and design ideas that i could implement into my application.

-Link: https://github.com/MaterialDesignInXAML/MaterialDesignInXamlToolkit/tree/master
-title: MaterialDesignInXamlToolKit
-This github readme contained a UI design toolkit which I incorporated into my app to give it its current look.



