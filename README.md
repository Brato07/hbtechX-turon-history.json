# hbtechX-turon-history.json

async function fetchXCPPrice() {
  const response = await fetch("https://api.coingecko.com/api/v3/simple/price?ids=counterparty&vs_currencies=usd");
  const data = await response.json();
  return data.counterparty.usd;
} 

async function renderChart() {
  const turonPriceUSD = 24.34; // Static TURON price from Counterparty
  const xcpPriceUSD = await fetchXCPPrice(); // Live XCP price
  const turonPriceXCP = turonPriceUSD / xcpPriceUSD;

  // Chart.js rendering logic here...
}  <div style="font-size: 12px; margin-top: 10px;">
  TURON is issued under UCC Article 9 and claims Basel-4 compliance. Not financial advice.
</div> const historicalData = [
  { date: "2025-09-06", price: 23.80 },
  { date: "2025-09-07", price: 24.10 },
  { date: "2025-09-08", price: 24.34 },
]; <select id="compareToken">
  <option value="xcp">XCP</option>
  <option value="btc">BTC</option>
  <option value="eth">ETH</option>
  <option value="gldb">GLDB</option>
</select>

<button onclick="toggleChart()">Toggle Historical View</button> <!DOCTYPE html>
<html>
<head>
  <title>TURON Price Widget</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <h2>TURON Price Comparison</h2>

  <select id="compareToken">
    <option value="xcp">XCP</option>
    <option value="btc">BTC</option>
    <option value="eth">ETH</option>
  </select>

  <button onclick="toggleChart()">Toggle Historical View</button>
  <canvas id="turonChart" width="600" height="400"></canvas>

  <div style="font-size: 12px; margin-top: 10px;">
    TURON is issued under UCC Article 9 and claims Basel-4 compliance. Not financial advice.
  </div>

  <script>
    let historicalMode = false;

    const historicalData = [
      { date: "2025-09-10", price: 23.80 },
      { date: "2025-09-11", price: 24.10 },
      { date: "2025-09-12", price: 24.34 }
    ];

    async function fetchTokenPrice(tokenId) {
      const url = `https://api.coingecko.com/api/v3/simple/price?ids=${tokenId}&vs_currencies=usd`;
      const response = await fetch(url);
      const data = await response.json();
      return data[tokenId].usd;
    }

    async function renderChart() {
      const turonPriceUSD = 24.34; // Static TURON price from Counterparty
      const selectedToken = document.getElementById("compareToken").value;
      const tokenMap = { xcp: "counterparty", btc: "bitcoin", eth: "ethereum" };
      const compareTokenId = tokenMap[selectedToken];
      const compareTokenPrice = await fetchTokenPrice(compareTokenId);
      const turonPriceInToken = turonPriceUSD / compareTokenPrice;

      const ctx = document.getElementById("turonChart").getContext("2d");

      const chartData = historicalMode
        ? {
            labels: historicalData.map(d => d.date),
            datasets: [{
              label: "TURON Price in USD",
              data: historicalData.map(d => d.price),
              borderColor: "rgba(46, 204, 113, 0.8)",
              backgroundColor: "rgba(46, 204, 113, 0.2)",
              fill: true,
              tension: 0.3
            }]
          }
        : {
            labels: ["TURON"],
            datasets: [
              {
                label: "Price in USD",
                data: [turonPriceUSD],
                backgroundColor: "rgba(46, 204, 113, 0.6)",
                yAxisID: "y",
              },
              {
                label: `Price in ${selectedToken.toUpperCase()}`,
                data: [turonPriceInToken],
                backgroundColor: "rgba(52, 152, 219, 0.6)",
                yAxisID: "y1",
              }
            ]
          };

      const chartOptions = historicalMode
        ? {
            responsive: true,
            scales: {
              y: {
                title: {
                  display: true,
                  text: "USD"
                }
              }
            }
          }
        : {
            responsive: true,
            scales: {
              y: {
                type: "linear",
                position: "left",
                title: {
                  display: true,
                  text: "USD"
                }
              },
              y1: {
                type: "linear",
                position: "right",
                title: {
                  display: true,
                  text: selectedToken.toUpperCase()
                },
                grid: {
                  drawOnChartArea: false
                }
              }
            }
          };

      if (window.myChart) window.myChart.destroy();
      window.myChart = new Chart(ctx, {
        type: historicalMode ? "line" : "bar",
        data: chartData,
        options: chartOptions
      });
    }

    function toggleChart() {
      historicalMode = !historicalMode;
      renderChart();
    }

    document.getElementById("compareToken").addEventListener("change", renderChart);
    renderChart();
  </script>
</body> async function fetchHistoricalTURON() {
  const response = await fetch("https://yourdomain.com/data/turon-history.json");
  const data = await response.json();
  return data;
}

async function renderHistoricalChart() {
  const data = await fetchHistoricalTURON();
  const ctx = document.getElementById("turonChart").getContext("2d");

  const labels = data.map(entry => entry.date);
  const prices = data.map(entry => entry.price_usd);

  if (window.myChart) window.myChart.destroy();
  window.myChart = new Chart(ctx, {
    type: "line",
    data: {
      labels: labels,
      datasets: [{
        label: "TURON Price (USD)",
        data: prices,
        borderColor: "rgba(46, 204, 113, 0.8)",
        backgroundColor: "rgba(46, 204, 113, 0.2)",
        fill: true,
        tension: 0.3
      }]
    },
    options: {
      responsive: true,
      scales: {
        y: {
          title: {
            display: true,
            text: "USD"
          }
        }
      }
    }
  });
} function toggleChart() {
  historicalMode = !historicalMode;
  if (historicalMode) {
    renderHistoricalChart();
  } else {
    renderChart(); // your current price chart
  }
} function toggleChart() {
  historicalMode = !historicalMode;
  if (historicalMode) {
    renderHistoricalChart();
  } else {
    renderChart(); // your current price chart
  }
}

