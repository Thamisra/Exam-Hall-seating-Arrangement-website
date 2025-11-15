<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exam Seating Arrangement</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #E69597;
            color: black;
            margin: 0;
            padding: 0;
            transition: background 0.3s, color 0.3s;
        }

        .dark-mode {
            background-color: #1e1e1e;
            color: white;
        }

        .container {
            margin-top: 50px;
            background: #ceb5b7;
            padding: 20px;
            width: 60%;
            margin-left: auto;
            margin-right: auto;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
            transition: background 0.3s;
        }

        .dark-mode .container {
            background: #333;
            color: white;
        }

        .toggle-btn {
            background: #222;
            color: white;
            padding: 10px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 150px;
            margin: auto;
        }

        .toggle-btn i {
            margin-left: 10px;
        }

        .toggle-btn:hover {
            background: #555;
        }

        .seating-chart {
            margin-top: 20px;
            display: none;
            flex-direction: column;
            align-items: center;
        }

        .bench {
            display: flex;
            justify-content: space-around;
            width: 60%;
            margin: 10px auto;
            padding: 10px;
            background: #ddd;
            border-radius: 5px;
            box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.1);
            transition: background 0.3s;
        }

        .dark-mode .bench {
            background: #444;
        }

        .seat {
            width: 50px;
            height: 50px;
            background: rgb(213, 200, 200);
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background 0.3s, transform 0.3s;
            font-weight: bold;
        }

        .dark-mode .seat {
            background: #666;
        }

        .seat:hover {
            background: #74b9ff;
            transform: scale(1.1);
        }

        .highlight {
            background: #2d3436;
            color: white;
            font-size: 22px;
            display: flex;
            justify-content: center;
            align-items: center;
            animation: flash 0.5s alternate 3;
        }

        .highlight i {
            font-size: 22px;
        }

        @keyframes flash {
            0% { background: #2d3436; }
            100% { background: #f1c40f; }
        }

        #clock {
            font-size: 20px;
            margin-top: 10px;
            font-weight: bold;
        }

    </style>
</head>
<body>

<button class="toggle-btn" onclick="toggleDarkMode()">Toggle Dark Mode <i class="fas fa-moon"></i></button>

<div class="container">
    <h2>Exam Seating Arrangement</h2>
    <div id="clock"></div>
    <p>Enter your Register Number to check your seat details.</p>
    <input type="text" id="registerNumber" placeholder="Enter Register Number">
    <button onclick="findSeat()">Check Seat</button>
    <div id="result" class="result"></div>
    <div class="seating-chart" id="seatingChart"></div>
</div>

<script>
    const seatingData = {
        "20231015": { hall: "Room 205", seat: 1, dept: "EC" },
        "20231016": { hall: "Room 205", seat: 2, dept: "CS" },
        "20231017": { hall: "Room 205", seat: 3, dept: "EC" },
        "20231018
