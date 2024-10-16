# Guvi_MongoDB_Task-CLI

## AIM:
To Design a database for Zen class programme and perform the following queries.

## Database Design:

![image](https://github.com/user-attachments/assets/27359846-f34e-476e-bf83-8f37b393a3af)

Under Guvi database, we have several collections :
  1.users
  2.codekata
  3.attendance
  4.topics
  5.tasks
  6.company_drives
  7.mentors

## Schema design of users:

```py

{
  "_id": {
    "type": "ObjectId",
    "description": "Unique identifier for the user document."
  },
  "name": {
    "type": "String",
    "description": "Name of the user."
  },
  "email": {
    "type": "String",
    "description": "Email address of the user."
  },
  "studentId": {
    "type": "String",
    "description": "Unique identifier assigned to the student."
  },
  "attendance": {
    "type": "Array",
    "items": {
      "type": "ObjectId",
      "description": "References to attendance documents in the attendance collection."
    },
    "description": "Array of ObjectIds pointing to attendance records."
  },
  "tasks": {
    "type": "Array",
    "items": {
      "type": "ObjectId",
      "description": "References to task documents in the tasks collection."
    },
    "description": "Array of ObjectIds pointing to tasks completed by the user."
  },
  "codekata": {
    "type": "ObjectId",
    "description": "Reference to the user's codekata document."
  },
  "mentor": {
    "type": "ObjectId",
    "description": "Reference to the mentor document."
  }
}

```
![image](https://github.com/user-attachments/assets/5f0b94a6-1952-49d6-94c3-9304c8abe4f8)


## Schema design of codekata

```py
{
  "_id": {
    "type": "ObjectId",
    "description": "Unique identifier for the codekata document."
  },
  "studentId": {
    "type": "String",
    "description": "Unique identifier assigned to the student."
  },
  "problems_solved": {
    "type": "String",
    "description": "Number of problems solved by the student in codekata."
  }
}


```
![image](https://github.com/user-attachments/assets/0b0e5fb0-cf41-4dcc-92bd-fa474e75f1e1)


## Schema design of attendance

```py
{
  "_id": {
    "type": "ObjectId",
    "description": "Unique identifier for the attendance document."
  },
  "presentStudentsId": {
    "type": "Array",
    "items": {
      "type": "String",
      "description": "Array of student IDs who were present on that date."
    },
    "description": "Array of student IDs who attended the class on the specific date."
  },
  "date": {
    "type": "Date",
    "description": "Date of the attendance record."
  }
}

```
![image](https://github.com/user-attachments/assets/3e696fad-ec70-4ecf-8763-37a0361ebb74)


## Schema design of topics

```py
{
  "_id": {
    "type": "ObjectId",
    "description": "Unique identifier for the topic document."
  },
  "name": {
    "type": "String",
    "description": "Name of the topic."
  },
  "date": {
    "type": "Date",
    "description": "Date when the topic was taught or created."
  },
  "relatedTasks": {
    "type": "ObjectId",
    "description": "Reference to a task associated with the topic."
  }
}


```
![image](https://github.com/user-attachments/assets/aa9aa7c1-360f-4e1e-b715-1e4e1c67c851)

## Schema design of tasks

```py
{
  "_id": {
    "type": "ObjectId",
    "description": "Unique identifier for the task document."
  },
  "taskNumber": {
    "type": "Number",
    "description": "Sequential number assigned to the task."
  },
  "submitted": {
    "type": "Array",
    "items": {
      "type": "String",
      "description": "Array of student IDs who submitted the task."
    },
    "description": "Array of student IDs who completed and submitted the task."
  },
  "notSubmitted": {
    "type": "Array",
    "items": {
      "type": "String",
      "description": "Array of student IDs who did not submit the task."
    },
    "description": "Array of student IDs who did not submit the task."
  },
  "date": {
    "type": "Date",
    "description": "Date when the task was assigned."
  },
  "taskDesc": {
    "type": "String",
    "description": "Description of the task."
  }
}

```
![image](https://github.com/user-attachments/assets/e67f8f57-133e-4cdc-b075-7fb83f0e20af)


## Schema design of company_drives

```py
{
  "_id": {
    "type": "ObjectId",
    "description": "Unique identifier for the company drive document."
  },
  "drive_name": {
    "type": "String",
    "description": "Name of the company drive (e.g., Google, Microsoft)."
  },
  "date": {
    "type": "Date",
    "description": "Date when the company drive took place."
  },
  "students_appeared": {
    "type": "Array",
    "items": {
      "type": "String",
      "description": "Array of student IDs who appeared for the drive."
    },
    "description": "Array of student IDs representing students who participated in the company drive."
  }
}


```
![image](https://github.com/user-attachments/assets/b234a7f6-bff4-4b6e-aa55-a411a2a35765)


## Schema design of mentors

```py
{
  "_id": {
    "type": "ObjectId",
    "description": "Unique identifier for the mentor document."
  },
  "name": {
    "type": "String",
    "description": "Name of the mentor (e.g., Nagarajan)."
  },
  "mentorid": {
    "type": "String",
    "description": "Unique identifier for the mentor (e.g., M100)."
  },
  "mentees": {
    "type": "Array",
    "items": {
      "type": "String",
      "description": "Array of student IDs representing the mentees assigned to the mentor."
    },
    "description": "Array of student IDs who are mentored by the mentor."
  }
}

```
![image](https://github.com/user-attachments/assets/56d9cb53-0472-4148-99b8-a6b4313f71bd)

## Queries:

### 1.Find all the topics and tasks which are thought in the month of October:

#### For separately finding the topics and tasks in October:
```py
// Find topics taught in October
db.topics.find({
    date: { $gte: ISODate("2020-10-01"), $lte: ISODate("2020-10-31") }
}).pretty();

// Find tasks taught in October
db.tasks.find({
    date: { $gte: ISODate("2020-10-01"), $lte: ISODate("2020-10-31") }
}).pretty();

```
![image](https://github.com/user-attachments/assets/58c92a61-314c-49c3-b8d2-a2acedb3f9de)
![image](https://github.com/user-attachments/assets/c1001944-72a0-42c1-8db8-4d804472fc73)


#### For finding Topics Taught in October with Related Tasks using LookUp:
```py
db.topics.aggregate([
    {
        $match: { // Match topics taught in October
            date: { $gte: ISODate("2020-10-01"), $lte: ISODate("2020-10-31") }
        }
    },
    {
        $lookup: {
            from: "tasks", // The collection to join
            localField: "_id", // Field from the topics collection
            foreignField: "relatedTasks", // Field from the tasks collection that references topics
            as: "relatedTasks" // Name of the new array field to add in the output
        }
    },
    {
        $project: {
            name: 1, // Include the topic name in the output
            date: 1, // Include the topic date in the output
            relatedTasks: 1 // Include the related tasks array in the output
        }
    }
]).pretty();


```
### 2.Find all the company drives which appeared between 15 oct-2020 and 31-oct-2020:
```py
db.company_drives.find({
    date: { $gte: ISODate("2020-10-15"), $lte: ISODate("2020-10-31") }
},{_id:0,students_appeared:0}).pretty();

```
![image](https://github.com/user-attachments/assets/57ec8597-deec-417d-b7dc-6930a78c5fbf)

### 3.Find all the company drives and students who are appeared for the placement:
```py
db.company_drives.aggregate([
    {
        $lookup: {
            from: "users", // Join with the users collection to get student details
            localField: "students_appeared", // Field in company_drives containing student IDs
            foreignField: "studentId", // Field in users that matches student IDs
            as: "studentDetails" // Output array will be named "studentDetails"
        }
    },
    {
        $project: {
            drive_name: 1, // Keep the drive name
            date: 1, // Keep the date of the drive
            studentDetails: { // Include the student details array
                $map: {
                    input: "$studentDetails", // Input from the studentDetails array
                    as: "student", // Alias for each student detail
                    in: {
                        studentId: "$$student.studentId", // Include studentId
                        name: "$$student.name", // Include student name
                        email: "$$student.email" // Include student email
                    }
                }
            }
        }
    }
]).pretty();

```
![image](https://github.com/user-attachments/assets/b7ae75ca-6884-419b-98b1-addbc05c5878)

### 4.Find the number of problems solved by the user in codekata:
```py
db.codekata.findOne(
    { studentId: "S12345" }, 
    { problems_solved: 1, _id: 0 } // Only return the problems_solved field and exclude the _id field
)

```
![image](https://github.com/user-attachments/assets/caf2a8fb-92ab-410d-941a-f090e8749249)

### 5.Find all the mentors with who has the mentee's count more than 15:
```py
db.mentors.find({
    $expr: { $gt: [{ $size: "$mentees" }, 15] } // Use $expr to evaluate the size of the mentees array
}).pretty();

```
### 6.Find the number of users who are absent and task is not submitted  between 15 oct-2020 and 31-oct-2020:
```py
db.users.aggregate([
    {
        $lookup: {
            from: "attendance", // Join with attendance collection
            localField: "attendance", // Field in users that contains attendance ObjectIds
            foreignField: "_id", // Match with the _id field in attendance documents
            as: "attendanceRecords" // Output array will be named "attendanceRecords"
        }
    },
    {
        $lookup: {
            from: "tasks", // Join with tasks collection
            localField: "tasks", // Field in users that contains tasks ObjectIds
            foreignField: "_id", // Match with the _id field in tasks documents
            as: "taskRecords" // Output array will be named "taskRecords"
        }
    },
    {
        $project: {
            name: 1,
            studentId: 1,
            absentDates: {
                $filter: {
                    input: "$attendanceRecords",
                    as: "record",
                    cond: {
                        $not: { $in: [ "$studentId", "$$record.presentStudentsId" ] } // Check if studentId is not in presentStudents
                    }
                }
            },
            notSubmittedTasks: {
                $filter: {
                    input: "$taskRecords",
                    as: "task",
                    cond: {
                        $and: [
                            { $eq: ["$$task.submitted", []] }, // Check if submitted array is empty
                            { $gte: ["$$task.date", ISODate("2020-10-15")] }, // Task date should be after October 15
                            { $lte: ["$$task.date", ISODate("2020-10-31")] } // Task date should be before October 31
                        ]
                    }
                }
            }
        }
    },
    {
        $match: {
            $and: [
                { "absentDates": { $ne: [] } }, // Match users with absent dates
                { "notSubmittedTasks": { $ne: [] } } // Match users with tasks not submitted
            ]
        }
    },
    {
        $count: "absentAndNotSubmittedCount" // Count the number of users who meet the criteria
    }
]).pretty();

```
![image](https://github.com/user-attachments/assets/52ec8d26-dc66-45cf-99a7-4b297e0700a2)

## Task time extension proof:

![image](https://github.com/ShakthiSundar-K/Guvi_D5_Task/assets/128116143/5318043f-5150-4178-bb8d-39bf235a2149)

