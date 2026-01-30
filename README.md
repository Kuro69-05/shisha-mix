<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Shisha Flavor Tracker</title>
  <style>
    body {
      font-family: system-ui, sans-serif;
      margin: 0;
      background: #0f172a;
      color: #e5e7eb;
    }
    header {
      padding: 16px;
      background: #020617;
      text-align: center;
      font-size: 20px;
      font-weight: bold;
    }
    .container {
      padding: 16px;
    }
    input, select {
      width: 100%;
      padding: 10px;
      margin-bottom: 12px;
      border-radius: 8px;
      border: none;
      font-size: 16px;
    }
    .flavor {
      background: #020617;
      padding: 12px;
      border-radius: 10px;
      margin-bottom: 10px;
    }
    .category {
      font-size: 12px;
      opacity: 0.7;
    }
  </style>
</head>
<body>

<header>🍃 Shisha Flavor Tracker</header>

<div class="container">
  <input type="text" id="search" placeholder="フレーバー名で検索">

  <select id="categoryFilter">
    <option value="all">すべてのカテゴリー</option>
    <option value="fruit">フルーツ</option>
    <option value="mint">ミント</option>
    <option value="tea">ティー</option>
    <option value="spice">スパイス</option>
    <option value="sweet">スイーツ</option>
  </select>

  <div id="flavorList"></div>
</div>

<script>
  const flavors = [
    { name: "ダブルアップル", category: "fruit" },
    { name: "ブルーベリー", category: "fruit" },
    { name: "スイートミント", category: "mint" },
    { name: "アールグレイ", category: "tea" },
    { name: "カルダモン", category: "spice" },
    { name: "バニラ", category: "sweet" }
  ];

  const flavorList = document.getElementById("flavorList");
  const searchInput = document.getElementById("search");
  const categoryFilter = document.getElementById("categoryFilter");

  function renderFlavors() {
    const search = searchInput.value.toLowerCase();
    const category = categoryFilter.value;

    flavorList.innerHTML = "";

    flavors
      .filter(f =>
        f.name.toLowerCase().includes(search) &&
        (category === "all" || f.category === category)
      )
      .forEach(f => {
        const div = document.createElement("div");
        div.className = "flavor";
        div.innerHTML = `
          <div>${f.name}</div>
          <div class="category">${f.category}</div>
        `;
        flavorList.appendChild(div);
      });
  }

  searchInput.addEventListener("input", renderFlavors);
  categoryFilter.addEventListener("change", renderFlavors);

  renderFlavors();
</script>

</body>
</html>
