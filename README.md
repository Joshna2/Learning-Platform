# Learning-Platform
javascript
import React, { useState, useEffect } from 'react';
import firebase from 'firebase';
function App() {
 const [courses, setCourses] = useState([]);
 useEffect(() => {
 firebase.database().ref('courses/').on('value', (snapshot) => {
 const courses = [];
 snapshot.forEach((childSnapshot) => {
 courses.push({
 id: childSnapshot.key,
 ...childSnapshot.val()
 });
 });
 setCourses(courses);
 });
 }, []);
 return (
 <div>
 <h1>E-Learning Platform</h1>
 <ul>
 {courses.map((course) => (
 <li key={course.id}>
 <>{course.title}</>
 <p>{course.description}</p>
 <button>Enroll</button>
 </li>
 ))}
 </ul>
 </div>
 );
}
export default App;
