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
            margin-top: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            width: 150px;
            margin: auto;
            position: absolute;
            bottom: 20px;
            right: 20px;
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

<button class="toggle-btn"  onclick="toggleDarkMode()">Toggle Dark Mode <i class="fas fa-moon"></i></button>

<div class="container">
    <h2>Exam Seating Arrangement</h2>
    <div id="clock"></div>
    <p>Enter your Register Number to check your seat details.</p>
    <input type="text" id="registerNumber" placeholder="Enter Register Number" aria-label="Enter your Register Number">
    <button onclick="findSeat()">Check Seat</button>
    <div id="result" class="result"></div>
    <div class="seating-chart" id="seatingChart"></div>
</div>

<script>
    // Sample data of seating arrangement
    const seatingData = {
        "20231015": { hall: "Room 205", seat: 1, dept: "EC" },
        "20231016": { hall: "Room 205", seat: 2, dept: "CS" },
        "20231017": { hall: "Room 205", seat: 3, dept: "EC" },
        "20231018": { hall: "Room 205", seat: 4, dept: "CS" },
        "20231019": { hall: "Room 205", seat: 5, dept: "EC" },
        "20231020": { hall: "Room 205", seat: 6, dept: "CS" },
        "20231021": { hall: "Room 205", seat: 7, dept: "EC" },
        "20231022": { hall: "Room 205", seat: 8, dept: "CS" },
        "20231023": { hall: "Room 205", seat: 9, dept: "EC" },
        "20231024": { hall: "Room 205", seat: 10, dept: "CS" }
    };

    // Function to generate seating chart
    function generateSeatingChart(highlightSeat = null) {
        let seatingChart = document.getElementById("seatingChart");
        seatingChart.innerHTML = "";  

        for (let i = 0; i < 5; i++) {
            let bench = document.createElement("div");
            bench.classList.add("bench");

            for (let j = 0; j < 2; j++) {
                let seatNumber = i * 2 + j + 1;
                let seat = document.createElement("div");
                seat.classList.add("seat");
                seat.innerText = seatNumber;

                // Highlight seat logic
                if (highlightSeat === seatNumber) {
                    seat.classList.add("highlight");
                    seat.innerHTML = '<i class="fas fa-user"></i>'
                }
                bench.appendChild(seat);
            }
            seatingChart.appendChild(bench);
        }
    }

    // Function to handle seat finding
    function findSeat() {
        let regNumber = document.getElementById("registerNumber").value.trim();
        let resultDiv = document.getElementById("result");
        let seatingChart = document.getElementById("seatingChart");

        if (seatingData[regNumber]) {
            let details = seatingData[regNumber];
            resultDiv.innerHTML = `<strong>Exam Hall:</strong> ${details.hall}<br>
                                   <strong>Seat Number:</strong> ${details.seat}<br>
                                   <strong>Department:</strong> ${details.dept}`;
            resultDiv.style.color = "green";
            resultDiv.style.padding = "20px";

            seatingChart.style.display = "block";  
            generateSeatingChart(details.seat);
        } else {
            resultDiv.innerHTML = "Register Number not found!";
            resultDiv.style.color = "red";
            seatingChart.style.display = "none";  
        }
    }

    // Dark mode toggle
    function toggleDarkMode() {
        document.body.classList.toggle("dark-mode");
    }

    // Function to update the clock
    function updateClock() {
        document.getElementById("clock").innerText = new Date().toLocaleTimeString();
        setTimeout(updateClock, 1000);
    }

    // Initialize clock
    updateClock();

    // Event listeners for dark mode toggle and seat checking
    document.getElementById("toggleDarkMode").addEventListener("click", toggleDarkMode);
    document.getElementById("checkSeatBtn").addEventListener("click", findSeat);
</script>

</body>
</html>

    
