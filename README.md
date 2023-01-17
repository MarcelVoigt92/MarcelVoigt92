# Aloha 🌊
- 👀 **I am currently in school to become a web developer**
```python
class marcel:
  def __init__(info):
    info.aboutme = {
            "email": ["marcel.voigt92@gmx.de"],
            "personal info": ["Marcel", "Voigt", "30", "Apache Attack Helicopter"],
            "portfolio": ["work in progress"],
            "location": ["Germany", "Niedersachsen"],
            "discord": ["Yukinoyo#2096"]
```

- 👌 Feel free to contact me

- I Work with: <br><br> <image src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" />
  <image src="https://img.shields.io/badge/CSS-239120?&style=for-the-badge&logo=css3&logoColor=white" />
  <image src="https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white">
  <image src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black">
  <image src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB">
  <image src="https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white">
  <image src="https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white"> <image src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white"> 


<a href="https://github.com/MarcelVoigt92">
  <img src="https://img.shields.io/github/followers/MarcelVoigt92">
</a>
<a href="https://github.com/MarcelVoigt92">
  <img src="https://img.shields.io/github/stars/MarcelVoigt92">
</a>
<!--
<image src="https://images-cdn.9gag.com/photo/aBnXd8z_700b.jpg">
<image src=""> -->
const balance = document.getElementById("balance");
const moneyPlus = document.getElementById("money-plus");
const moneyMinus = document.getElementById("money-minus");
const list = document.getElementById("list");
const form = document.getElementById("form");
const text = document.getElementById("text");
const amount = document.getElementById("amount");
const notification = document.getElementById("notification");

const dummyTransactions = [
  { id: 1, text: "Flower", amount: -20 },
  { id: 2, text: "Salary", amount: 300 },
  { id: 3, text: "Book", amount: -10 },
  { id: 4, text: "Camera", amount: 150 },
];

let transactions = dummyTransactions;

// LocalStorage is not enabled in CodePen for security reasons
// const localStorageTransactions = JSON.parse(
//   localStorage.getItem("transactions")
// );
// let transactions =
//   localStorageTransactions !== null ? localStorageTransactions : [];

// function updateLocaleStorage() {
//   localStorage.setItem("transactions", JSON.stringify(transactions));
// }

function showNotification() {
  notification.classList.add("show");
  setTimeout(() => {
    notification.classList.remove("show");
  }, 2000);
}

function generateID() {
  return Math.floor(Math.random() * 100000000);
}

function addTransaction(e) {
  e.preventDefault();
  if (text.value.trim() === "" || amount.value.trim() === "") {
    showNotification();
  } else {
    const transaction = {
      id: generateID(),
      text: text.value,
      amount: +amount.value,
    };
    transactions.push(transaction);
    addTransactionDOM(transaction);
    updateValues();
    // updateLocaleStorage();
    text.value = "";
    amount.value = "";
  }
}

function addTransactionDOM(transaction) {
  const sign = transaction.amount < 0 ? "-" : "+";
  const item = document.createElement("li");
  item.classList.add(sign === "+" ? "plus" : "minus");
  item.innerHTML = `
          ${transaction.text} <span>${sign}${Math.abs(transaction.amount)}</span
          ><button class="delete-btn" onclick="removeTransaction(${
            transaction.id
          })"><i class="fa fa-times"></i></button>
    `;
  list.appendChild(item);
}

function updateValues() {
  const amounts = transactions.map((transaction) => transaction.amount);
  const total = amounts
    .reduce((accumulator, value) => (accumulator += value), 0)
    .toFixed(2);
  const income = amounts
    .filter((value) => value > 0)
    .reduce((accumulator, value) => (accumulator += value), 0)
    .toFixed(2);
  const expense = (
    amounts
      .filter((value) => value < 0)
      .reduce((accumulator, value) => (accumulator += value), 0) * -1
  ).toFixed(2);
  balance.innerText = `€${total}`;
  moneyPlus.innerText = `€${income}`;
  moneyMinus.innerText = `€${expense}`;
}

function removeTransaction(id) {
  transactions = transactions.filter((transaction) => transaction.id !== id);
  // updateLocaleStorage();
  init();
}

// Init
function init() {
  list.innerHTML = "";
  transactions.forEach(addTransactionDOM);
  updateValues();
}

init();

form.addEventListener("submit", addTransaction);
