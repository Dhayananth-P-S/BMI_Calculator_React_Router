# Ex06 BMI Calculator

## AIM
To develop a responsive and interactive Body Mass Index (BMI) Calculator using React that allows users to input their height and weight, and calculates their BMI to categorize their health status (e.g., Underweight, Normal, Overweight, Obese).

## DESIGN STEPS

### STEP 1: Initialize React Project

<li>Create a new React app using create-react-app.</li>
<li>Install React Router using:</li>
npm install react-router-dom

### STEP 2: Set Up Routing

Create routing structure with react-router-dom:

<li>Home route (/) – Intro or Navigation</li>

<li>BMI Calculator route (/bmi)</li>

<li>Result route (/result)</li>

### STEP 3: Design the BMI Form Page

<li>Create a form to accept Height (in cm or m) and Weight (in kg).</li>

<li>On form submit, navigate to the result page with entered values via URL query params or context/state.</li>

## STEP 4: Handle Input Validation

<li>Check if height and weight are valid numbers.</li>

<li>Optionally, show error messages for invalid inputs.</li>

### STEP 5: Perform BMI Calculation

<li>In the result component:

<li>Extract height and weight from the route (URL or passed state).</li>

<li>Apply the BMI formula:</li>

![image](https://github.com/user-attachments/assets/ec785506-c96b-489e-8783-fb1a5d36101a)
​
 
<li>Convert height from cm to m if needed.</li></li>

### STEP 6: Display Result

<li>Show calculated BMI.</li>

<li>Show category based on BMI range:

<li>Underweight, Normal, Overweight, Obese, etc.</li></li>

### STEP 7: Navigation Options

<li>Provide a button to go back to the BMI form to calculate again.</li>

### STEP 8: Enhancements

<li>Add styling using CSS or Tailwind.</li>

## PROGRAM
# index.jss
```.js
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<App />);
```
# App.js
```.js
import { BrowserRouter as Router, Routes, Route } from "react-router-dom";
import Home from "./Home";
import BMIForm from "./BMIForm";
import Result from "./Result";

function App() {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/bmi" element={<BMIForm />} />
        <Route path="/result" element={<Result />} />
      </Routes>
    </Router>
  );
}

export default App;
```
# Home.js
```.js
import { useNavigate } from "react-router-dom";

export default function Home() {
  const navigate = useNavigate();

  return (
    <div style={{ textAlign: "center", marginTop: "100px" }}>
      <h1>BMI Calculator</h1>
      <button onClick={() => navigate("/bmi")}>
        Go to Calculator
      </button>
    </div>
  );
}
```
# BMIForm.js
```.js
import { useState } from "react";
import { useNavigate } from "react-router-dom";

export default function BMIForm() {
  const [height, setHeight] = useState("");
  const [weight, setWeight] = useState("");
  const [error, setError] = useState("");

  const navigate = useNavigate();

  const handleSubmit = (e) => {
    e.preventDefault();

    if (!height || !weight || isNaN(height) || isNaN(weight)) {
      setError("Enter valid numbers");
      return;
    }

    navigate("/result", {
      state: { height, weight }
    });
  };

  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h2>Enter Details</h2>

      <form onSubmit={handleSubmit}>
        <input
          type="text"
          placeholder="Height (cm)"
          value={height}
          onChange={(e) => setHeight(e.target.value)}
        />
        <br /><br />

        <input
          type="text"
          placeholder="Weight (kg)"
          value={weight}
          onChange={(e) => setWeight(e.target.value)}
        />
        <br /><br />

        <button type="submit">Calculate BMI</button>
      </form>

      {error && <p style={{ color: "red" }}>{error}</p>}
    </div>
  );
}
```
# Result.js
```.js
import { useLocation, useNavigate } from "react-router-dom";

export default function Result() {
  const location = useLocation();
  const navigate = useNavigate();

  const { height, weight } = location.state || {};

  if (!height || !weight) {
    return <p>No data found</p>;
  }

  const h = height / 100;
  const bmi = (weight / (h * h)).toFixed(2);

  let category = "";

  if (bmi < 18.5) category = "Underweight";
  else if (bmi < 24.9) category = "Normal";
  else if (bmi < 29.9) category = "Overweight";
  else category = "Obese";

  return (
    <div style={{ textAlign: "center", marginTop: "50px" }}>
      <h2>Your BMI: {bmi}</h2>
      <h3>{category}</h3>

      <button onClick={() => navigate("/bmi")}>
        Calculate Again
      </button>
    </div>
  );
}
```

## OUTPUT

<img width="796" height="316" alt="Screenshot 2026-03-19 112428" src="https://github.com/user-attachments/assets/1dead409-0b48-4b55-8bfb-e972ea13794b" />

<img width="667" height="334" alt="Screenshot 2026-03-19 112438" src="https://github.com/user-attachments/assets/98b88f30-b9a4-40e5-b8eb-3a43fe98dace" />


## RESULT
The BMI Calculator successfully takes user input for height and weight, performs the BMI calculation in real-time using React state and event handling, and displays the BMI value along with the corresponding health category.
