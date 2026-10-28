# School Management System

A comprehensive web-based School Management System built with Node.js, Express, SQLite, and vanilla JavaScript.

## Features

- **Student Management**: Add, view, update, and delete student records
- **Teacher Management**: Manage teacher information and qualifications
- **Class Management**: Create and manage classes with grade levels
- **Grades Management**: Record and track student grades by subject and term
- **Attendance Tracking**: Mark and monitor student attendance with statistics
- **User Authentication**: Secure login system with JWT tokens (Admin, Teacher, Student roles)
- **Dashboard**: Quick overview of system statistics and quick actions
- **Responsive Design**: Mobile-friendly interface

## System Requirements

- Node.js (v14 or higher)
- npm (Node Package Manager)
- Windows, macOS, or Linux

## Installation

### 1. Install Dependencies

```bash
npm install
```

This will install the following dependencies:
- `express` - Web framework
- `sqlite3` - Database
- `cors` - Cross-Origin Resource Sharing
- `body-parser` - Middleware for parsing request bodies
- `bcryptjs` - Password hashing
- `jsonwebtoken` - JWT authentication
- `dotenv` - Environment variables management

### 2. Start the Server

```bash
npm start
```

For development with auto-reload:
```bash
npm run dev
```

The server will start on `http://localhost:5000`

## Usage

### First Time Setup

1. Open your browser and go to `http://localhost:5000`
2. Use the demo credentials:
   - **Admin Login**: Username: `admin`, Password: `admin`
   - **Teacher Login**: Username: `teacher`, Password: `teacher`
   - **Student Login**: Username: `student`, Password: `student`

### Main Features

#### Dashboard
- View summary statistics (total students, teachers, classes, users)
- Quick access to main functions

#### Students
- Add new student records with personal and parent information
- View all students in a table format
- Delete student records

#### Teachers
- Add teacher information including qualifications and department
- Manage teacher records
- Track teacher assignments to classes

#### Classes
- Create new classes with grade levels
- Assign teachers to classes
- Set class capacity
- View students in each class

#### Grades
- Record student grades for different subjects
- Automatic grade calculation (A, B, C, D, F based on marks)
- Filter by student or class
- Support for multiple terms

#### Attendance
- Mark attendance for entire classes
- Track attendance status (Present, Absent, Late)
- View attendance statistics per student
- Bulk mark attendance for multiple students

## Project Structure

```
SCHOOL MANAGEMENT SYSTEM/
├── backend/
│   ├── database/
│   │   └── db.js              # Database initialization and schema
│   └── routes/
│       ├── students.js        # Student API routes
│       ├── teachers.js        # Teacher API routes
│       ├── classes.js         # Class API routes
│       ├── grades.js          # Grades API routes
│       ├── attendance.js      # Attendance API routes
│       └── users.js           # User authentication routes
├── public/
│   ├── index.html            # Main HTML file
│   ├── styles.css            # CSS styling
│   └── script.js             # Frontend JavaScript
├── server.js                 # Express server setup
├── package.json              # Project dependencies
├── .env                      # Environment variables
└── README.md                 # This file
```

## API Endpoints

### Students
- `GET /api/students` - Get all students
- `GET /api/students/:id` - Get student by ID
- `POST /api/students` - Add new student
- `PUT /api/students/:id` - Update student
- `DELETE /api/students/:id` - Delete student

### Teachers
- `GET /api/teachers` - Get all teachers
- `GET /api/teachers/:id` - Get teacher by ID
- `POST /api/teachers` - Add new teacher
- `PUT /api/teachers/:id` - Update teacher
- `DELETE /api/teachers/:id` - Delete teacher

### Classes
- `GET /api/classes` - Get all classes
- `GET /api/classes/:id` - Get class by ID
- `GET /api/classes/:id/students` - Get students in a class
- `POST /api/classes` - Add new class
- `PUT /api/classes/:id` - Update class
- `DELETE /api/classes/:id` - Delete class

### Grades
- `GET /api/grades` - Get all grades
- `GET /api/grades/student/:studentId` - Get grades for a student
- `GET /api/grades/class/:classId` - Get grades for a class
- `POST /api/grades` - Add new grade
- `PUT /api/grades/:id` - Update grade
- `DELETE /api/grades/:id` - Delete grade

### Attendance
- `GET /api/attendance` - Get all attendance records
- `GET /api/attendance/student/:studentId` - Get student attendance
- `GET /api/attendance/class/:classId/date/:date` - Get class attendance for a date
- `GET /api/attendance/stats/student/:studentId` - Get attendance statistics
- `POST /api/attendance` - Mark attendance
- `POST /api/attendance/bulk` - Bulk mark attendance
- `DELETE /api/attendance/:id` - Delete attendance record

### Users
- `POST /api/users/register` - Register new user
- `POST /api/users/login` - Login user
- `GET /api/users` - Get all users
- `GET /api/users/:id` - Get user by ID
- `PUT /api/users/:id` - Update user
- `POST /api/users/:id/change-password` - Change password
- `DELETE /api/users/:id` - Delete user

## Database Schema

### Users Table
- id (Primary Key)
- username (Unique)
- password (Hashed)
- role (admin, teacher, student)
- email
- created_at

### Students Table
- id (Primary Key)
- user_id (Foreign Key)
- first_name
- last_name
- date_of_birth
- gender
- enrollment_date
- phone
- address
- parent_name
- parent_phone

### Teachers Table
- id (Primary Key)
- user_id (Foreign Key)
- first_name
- last_name
- date_of_birth
- gender
- hiring_date
- phone
- address
- qualifications
- department

### Classes Table
- id (Primary Key)
- name
- grade_level
- teacher_id (Foreign Key)
- capacity

### Grades Table
- id (Primary Key)
- student_id (Foreign Key)
- class_id (Foreign Key)
- subject
- marks
- total_marks
- grade
- term
- recorded_date

### Attendance Table
- id (Primary Key)
- student_id (Foreign Key)
- class_id (Foreign Key)
- attendance_date
- status (present, absent, late)
- recorded_by
- remarks
- created_at

## Environment Variables

Create or modify `.env` file in the root directory:

```
PORT=5000
NODE_ENV=development
JWT_SECRET=your_super_secret_key_change_this_in_production
DATABASE_PATH=./backend/database/school.db
```

## Security Notes

1. **Change JWT Secret**: Always change the `JWT_SECRET` in production
2. **CORS Configuration**: Modify CORS settings if needed in `server.js`
3. **Password Storage**: Passwords are hashed using bcryptjs
4. **Database Location**: SQLite database is stored locally at `backend/database/school.db`

## Troubleshooting

### Port Already in Use
Change the `PORT` variable in `.env` file or use a different port:
```bash
PORT=3000 npm start
```

### Database Issues
Delete the `backend/database/school.db` file to reset the database:
```bash
rm backend/database/school.db
npm start
```

### Authentication Issues
Clear browser localStorage and login again:
1. Open Developer Tools (F12)
2. Go to Application > Local Storage
3. Delete all items
4. Refresh and login again

## Future Enhancements

- Email notifications for attendance and grades
- Advanced reporting and analytics
- Timetable management
- Exam scheduling
- Payment management
- Parent portal
- Mobile app
- Multi-language support
- Backup and restore functionality

## License

This project is open source and available for educational purposes.

## Support

For issues or questions, please refer to the code documentation or create an issue in the project repository.

## Authors

School Management System Development Team

---

**Last Updated**: February 14, 2026
#   s c h o o l - m a n a g e m e n t - s y s t e m 2  
 