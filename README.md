# Municipal Services Application - We Got You

## Overview
"We Got You" is a Municipal Services Application designed to streamline the reporting and management of municipal service requests. It allows users to submit issues, track their status, provide feedback, and view local events and announcements. This document serves as a comprehensive guide on compiling, running, and using the program, including explanations for the data structures used, with a focus on their role in the "Service Request Status" feature.

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
  
### Running the Application
1. Click `Start` or press `F5` within Visual Studio to launch the application.
2. Alternatively, navigate to the `bin/Debug` or `bin/Release` folder and execute the `.exe` file.

---

## How to Use the Application

### Main Menu
The main menu serves as the central hub for accessing various features:
- **Report Issues**: Navigate to a form where you can report municipal issues such as water leaks, potholes, etc.
- **Local Events and Announcements**: View upcoming events, important announcements, and community updates.
- **Provide Feedback**: Use in-app forms to provide feedback on municipal services or other features.

### Reporting Issues
1. Click the "Report Issues" button from the Main Menu.
2. Fill out the required fields:
   - **Location**: Enter the location of the issue.
   - **Category**: Select a category (e.g., Environment, Infrastructure).
   - **Priority**: Specify the priority (e.g., High, Medium, Low).
   - **Description**: Provide a detailed description of the issue.
3. Attach relevant media files (e.g., photos of the issue) using the "Attach File" button.
4. Submit the form by clicking "Submit," which generates a unique `RequestId` for tracking.
5. Optionally, clear and reset the form using the "Clear" button or return to the Main Menu using the "Back" button.

### Viewing Service Request Status
1. Navigate to the "Service Requests" section from the Main Menu.
2. Enter the `RequestId` to view the current status of your request.
3. The status, date of submission, and any updates will be displayed.

### Providing Feedback
1. Click the "Provide Feedback" button on the Main Menu.
2. Complete the feedback form:
   - **Rating**: Provide a rating using the rating system.
   - **Comments**: Optionally, add comments.
3. Submit your feedback, and you will receive a thank-you message.

### Local Events and Announcements
1. Click the "Local Events and Announcements" button.
2. Browse upcoming events and announcements.
3. Use the filter button to sort events by category or date, or search for specific events using the search bar.

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

#### Example:
```csharp
Dictionary<string, ServiceRequest> serviceRequestDict = new Dictionary<string, ServiceRequest>();

// Adding a service request to the dictionary
serviceRequestDict[report.RequestId] = newRequest;

// Retrieving and updating a request
if (serviceRequestDict.TryGetValue("SR001", out ServiceRequest request))
{
    request.Status = "Resolved";
}
```

### 3. **Queue**
#### Role and Contribution
- **Purpose**: Manages the processing order of pending service requests, ensuring a first-come, first-served system.
- **Usage**: New service requests are enqueued and processed in the order they are received.
- **Efficiency**: Provides constant-time enqueue and dequeue operations (`O(1)`), supporting fair request handling.

#### Example:
```csharp
Queue<ServiceRequest> requestQueue = new Queue<ServiceRequest>();

// Enqueuing a new request
requestQueue.Enqueue(newRequest);

// Dequeueing for processing
ServiceRequest nextRequest = requestQueue.Dequeue();
nextRequest.Status = "In Progress";
```

### 4. **SortedDictionary**
#### Role and Contribution
- **Purpose**: Maintains service requests in sorted order based on keys (e.g., request dates).
- **Usage**: Useful for scenarios where sorting based on request creation timestamps is needed.
- **Efficiency**: Provides `O(log n)` time complexity for insertion and lookup operations, offering a balance between speed and order preservation.

#### Example:

SortedDictionary<DateTime, ServiceRequest> sortedRequests = new SortedDictionary<DateTime, ServiceRequest>();

// Adding a service request
sortedRequests[newRequest.ReportedAt] = newRequest;

// Iterating over sorted requests
foreach (var entry in sortedRequests)
{
    Console.WriteLine($"Request ID: {entry.Value.RequestId}, Status: {entry.Value.Status}");
}
```

---


## Smart Recommendations and Local Events Feature(Updated)
The "Smart Recommendations" feature analyzes user search history and preferences using data structures like sets or custom algorithms to suggest relevant events.
this feature has been updated from the previous part- the Smart recommendations list accumulates rather than reseting after searching for different events. 
---

## Code Attribution
- Video Title: C# WPF UI | How to Design Input Form in WPF | Data Entry Form App
- Author: C# WPF UI Academy
- Published: 29 April 2022
- I used this video for inspiration and design ideas that i could implement into my application.

-Link: https://github.com/MaterialDesignInXAML/MaterialDesignInXamlToolkit/tree/master
-title: MaterialDesignInXamlToolKit
-This github readme contained a UI design toolkit which I incorporated into my app to give it its current look.



