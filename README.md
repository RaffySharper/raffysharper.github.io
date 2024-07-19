<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Football Stats</title>
  <style>
    body { font-family: Arial, sans-serif; }
    .stats { margin: 20px; }
    button { margin: 5px; }
  </style>
</head>
<body>
  <div class="stats">
    <h1>Football Stats</h1>
    <p>Matches Played: <span id="matches_played">0</span></p>
    <p>Goals Scored: <span id="goals_scored">0</span></p>
    <p>Goals Conceded: <span id="goals_conceded">0</span></p>
    <button onclick="increment('matches_played')">+1 Match Played</button>
    <button onclick="increment('goals_scored')">+1 Goal Scored</button>
    <button onclick="increment('goals_conceded')">+1 Goal Conceded</button>
  </div>
  
  <script>
    async function fetchStats() {
      const response = await fetch('http://localhost:3000/stats');
      const stats = await response.json();
      document.getElementById('matches_played').textContent = stats.matches_played;
      document.getElementById('goals_scored').textContent = stats.goals_scored;
      document.getElementById('goals_conceded').textContent = stats.goals_conceded;
    }

    async function increment(column) {
      await fetch('http://localhost:3000/increment', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ column })
      });
      fetchStats();
    }

    fetchStats();
  </script>
</body>
</html>
