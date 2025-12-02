<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Attendance System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 12px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .header p {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .content {
            padding: 30px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }

        @media (max-width: 768px) {
            .content {
                grid-template-columns: 1fr;
            }
        }

        .section {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .section-title {
            font-size: 1.5em;
            color: #333;
            font-weight: 600;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
        }

        .input-group {
            display: flex;
            gap: 10px;
        }

        input[type="text"] {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1em;
            transition: border-color 0.3s;
        }

        input[type="text"]:focus {
            outline: none;
            border-color: #667eea;
        }

        button {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-size: 1em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }

        .btn-primary {
            background: #667eea;
            color: white;
        }

        .btn-primary:hover {
            background: #5568d3;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .btn-present {
            background: #48bb78;
            color: white;
            flex: 1;
        }

        .btn-present:hover {
            background: #38a169;
        }

        .btn-present.active {
            background: #2f855a;
        }

        .btn-absent {
            background: #f56565;
            color: white;
            flex: 1;
        }

        .btn-absent:hover {
            background: #e53e3e;
        }

        .btn-absent.active {
            background: #c53030;
        }

        .btn-late {
            background: #ed8936;
            color: white;
            flex: 1;
        }

        .btn-late:hover {
            background: #dd6b20;
        }

        .btn-late.active {
            background: #c05621;
        }

        .btn-remove {
            background: #cbd5e0;
            color: #2d3748;
            padding: 8px 16px;
            font-size: 0.9em;
        }

        .btn-remove:hover {
            background: #a0aec0;
        }

        .student-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
            max-height: 500px;
            overflow-y: auto;
        }

        .student-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 15px;
            background: #f7fafc;
            border-radius: 8px;
            border: 1px solid #e2e8f0;
            transition: all 0.3s;
        }

        .student-item:hover {
            background: #edf2f7;
            border-color: #cbd5e0;
        }

        .student-name {
            flex: 1;
            font-weight: 500;
            color: #2d3748;
        }

        .attendance-status {
            display: flex;
            gap: 8px;
            align-items: center;
        }

        .status-badge {
            width: 24px;
            height: 24px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.75em;
            font-weight: bold;
            color: white;
        }

        .status-badge.present {
            background: #48bb78;
        }

        .status-badge.absent {
            background: #f56565;
        }

        .status-badge.late {
            background: #ed8936;
        }

        .status-badge.unmarked {
            background: #cbd5e0;
        }

        .student-buttons {
            display: flex;
            gap: 6px;
        }

        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }

        .stat-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
        }

        .stat-card.green {
            background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
            box-shadow: 0 4px 12px rgba(72, 187, 120, 0.3);
        }

        .stat-card.red {
            background: linear-gradient(135deg, #f56565 0%, #e53e3e 100%);
            box-shadow: 0 4px 12px rgba(245, 101, 101, 0.3);
        }

        .stat-card.orange {
            background: linear-gradient(135deg, #ed8936 0%, #dd6b20 100%);
            box-shadow: 0 4px 12px rgba(237, 137, 54, 0.3);
        }

        .stat-number {
            font-size: 2em;
            font-weight: bold;
        }

        .stat-label {
            font-size: 0.9em;
            opacity: 0.9;
        }

        .btn-export {
            background: #667eea;
            color: white;
            margin-top: 15px;
            width: 100%;
        }

        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: #718096;
        }

        .empty-state p {
            font-size: 1.1em;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📚 Student Attendance System</h1>
            <p>Track and manage student attendance with ease</p>
        </div>

        <div class="content">
            <!-- Left Column: Add Students & List -->
            <div class="section">
                <h2 class="section-title">Add Student</h2>
                <div class="input-group">
                    <input 
                        type="text" 
                        id="studentName" 
                        placeholder="Enter student name..." 
                        onkeypress="handleKeyPress(event)"
                    >
                    <button class="btn-primary" onclick="addStudent()">Add</button>
                </div>

                <h2 class="section-title">Student List</h2>
                <div id="studentList" class="student-list">
                    <div class="empty-state">
                        <p>No students added yet. Add one to get started!</p>
                    </div>
                </div>
            </div>

            <!-- Right Column: Statistics -->
            <div class="section">
                <h2 class="section-title">Attendance Statistics</h2>
                <div class="stats-container" id="statsContainer">
                    <div class="stat-card">
                        <div class="stat-number" id="totalCount">0</div>
                        <div class="stat-label">Total Students</div>
                    </div>
                    <div class="stat-card green">
                        <div class="stat-number" id="presentCount">0</div>
                        <div class="stat-label">Present</div>
                    </div>
                    <div class="stat-card red">
                        <div class="stat-number" id="absentCount">0</div>
                        <div class="stat-label">Absent</div>
                    </div>
                    <div class="stat-card orange">
                        <div class="stat-number" id="lateCount">0</div>
                        <div class="stat-label">Late</div>
                    </div>
                </div>

                <h2 class="section-title" style="margin-top: 30px;">Actions</h2>
                <button class="btn-export" onclick="exportToCSV()">📥 Export as CSV</button>
                <button class="btn-export" onclick="clearAllData()" style="background: #f56565; margin-top: 10px;">🗑️ Clear All Data</button>
            </div>
        </div>
    </div>

    <script>
        // Load data from localStorage
        function loadData() {
            const data = localStorage.getItem('attendanceData');
            return data ? JSON.parse(data) : [];
        }

        // Save data to localStorage
        function saveData(students) {
            localStorage.setItem('attendanceData', JSON.stringify(students));
        }

        // Add student
        function addStudent() {
            const nameInput = document.getElementById('studentName');
            const name = nameInput.value.trim();

            if (!name) {
                alert('Please enter a student name');
                return;
            }

            const students = loadData();
            
            if (students.some(s => s.name.toLowerCase() === name.toLowerCase())) {
                alert('Student already exists');
                return;
            }

            students.push({
                id: Date.now(),
                name: name,
                status: 'unmarked' // unmarked, present, absent, late
            });

            saveData(students);
            nameInput.value = '';
            renderStudents();
            updateStats();
        }

        // Handle Enter key press
        function handleKeyPress(event) {
            if (event.key === 'Enter') {
                addStudent();
            }
        }

        // Mark attendance
        function markAttendance(studentId, status) {
            const students = loadData();
            const student = students.find(s => s.id === studentId);
            if (student) {
                student.status = student.status === status ? 'unmarked' : status;
                saveData(students);
                renderStudents();
                updateStats();
            }
        }

        // Remove student
        function removeStudent(studentId) {
            if (confirm('Are you sure you want to remove this student?')) {
                const students = loadData().filter(s => s.id !== studentId);
                saveData(students);
                renderStudents();
                updateStats();
            }
        }

        // Render students list
        function renderStudents() {
            const students = loadData();
            const listContainer = document.getElementById('studentList');

            if (students.length === 0) {
                listContainer.innerHTML = '<div class="empty-state"><p>No students added yet. Add one to get started!</p></div>';
                return;
            }

            listContainer.innerHTML = students.map(student => `
                <div class="student-item">
                    <div class="student-name">${student.name}</div>
                    <div class="attendance-status">
                        <div class="status-badge ${student.status}">
                            ${student.status === 'present' ? '✓' : 
                              student.status === 'absent' ? '✗' : 
                              student.status === 'late' ? 'L' : '○'}
                        </div>
                    </div>
                    <div class="student-buttons">
                        <button class="btn-present ${student.status === 'present' ? 'active' : ''}" 
                                onclick="markAttendance(${student.id}, 'present')">Present</button>
                        <button class="btn-absent ${student.status === 'absent' ? 'active' : ''}" 
                                onclick="markAttendance(${student.id}, 'absent')">Absent</button>
                        <button class="btn-late ${student.status === 'late' ? 'active' : ''}" 
                                onclick="markAttendance(${student.id}, 'late')">Late</button>
                        <button class="btn-remove" onclick="removeStudent(${student.id})">Remove</button>
                    </div>
                </div>
            `).join('');
        }

        // Update statistics
        function updateStats() {
            const students = loadData();
            const total = students.length;
            const present = students.filter(s => s.status === 'present').length;
            const absent = students.filter(s => s.status === 'absent').length;
            const late = students.filter(s => s.status === 'late').length;

            document.getElementById('totalCount').textContent = total;
            document.getElementById('presentCount').textContent = present;
            document.getElementById('absentCount').textContent = absent;
            document.getElementById('lateCount').textContent = late;
        }

        // Export to CSV
        function exportToCSV() {
            const students = loadData();
            if (students.length === 0) {
                alert('No data to export');
                return;
            }

            let csv = 'Name,Status\n';
            students.forEach(student => {
                csv += `${student.name},${student.status}\n`;
            });

            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `attendance_${new Date().toISOString().split('T')[0]}.csv`;
            a.click();
        }

        // Clear all data
        function clearAllData() {
            if (confirm('Are you sure you want to clear all attendance data? This cannot be undone.')) {
                localStorage.removeItem('attendanceData');
                renderStudents();
                updateStats();
            }
        }

        // Initialize on page load
        window.addEventListener('load', () => {
            renderStudents();
            updateStats();
        });
    </script>
</body>
</html>
