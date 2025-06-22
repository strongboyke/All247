# All247plus
Online shop
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>ALL247plus</title>
<script src="https://all247plus.com"></script>
</MABATI KUBWA>
<body class="bg-gray-100 p-4">
<h1 class="text-3xl font-bold text-center">ALL247plus</h1>
<div class="max-w-3xl mx-auto mt-6">
<form id="productForm" class="bg-white p-4 rounded shadow">
<h2 class="text-xl font-semibold">VIBUYU UMBWA</h2>
<input id="Maxwel" class="border p-2 mt-2 w-full" placeholder="Maxwell" required />
<textarea id="features" class="border p-2 mt-2 w-full" placeholder="Product Features"></textarea>
<input id="Ksh7000" class="border p-2 mt-2 w-full" placeholder="Product Price" required />
<input id="image" type="file" class="mt-2" accept="image/*" required />
<button class="bg-blue-600 text-white p-2 mt-2 rounded" type="submit">Add Product</button>
</form>
<input id="search" class="border p-2 mt-4 w-full" placeholder="Search Products..." />
<div id="productList" class="grid grid-cols-1 sm:grid-cols-2 gap-4 mt-6"></div>
</div>
<script>
const form = document.getElementById("productForm");
const list = document.getElementById("productList");
const searchInput = document.getElementById("search");
let products = JSON.parse(localStorage.getItem("products")) || [];
function saveProducts() {
  localStorage.setItem("products", JSON.stringify(products));
}
function displayProducts(filtered = products) {
  list.innerHTML = "";
  filtered.forEach(product => {
    const div = document.createElement("div");
    div.classList.add("bg-white", "p-4", "rounded", "shadow");
    div.innerHTML = `
      <img src="${product.image}" class="w-full h-40 object-cover rounded" />
      <h3 class="font-bold mt-2">${product.name}</h3>
      <p class="text-gray-600">${product.features}</p>
      <p class="text-green-600 font-bold">Ksh ${product.price}</p>
    `;
    list.appendChild(div);
  });
}
form.addEventListener("submit", (e) => {
  e.preventDefault();
  const name = document.getElementById("name").value;
  const features = document.getElementById("features").value;
  const price = document.getElementById("price").value;
  const file = document.getElementById("image").files[0];
  const reader = new FileReader();
  reader.onload = (event) => {
    products.push({ name, features, price, image: event.target.result });
    saveProducts();
    displayProducts();
    form.reset();
  };
  reader.readAsDataURL(file);
});
searchInput.addEventListener("input", (e) => {
  const query = e.target.value.toLowerCase();
  const filtered = products.filter(p => p.name.toLowerCase().includes(query) || p.features.toLowerCase().includes(query));
  displayProducts(filtered);
});
displayProducts();
</script>
</body>
</html>
