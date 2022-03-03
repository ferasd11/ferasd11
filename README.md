- 👋 Hi, I’m @ferasd11
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
ferasd11/ferasd11 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
   <!DOCTYPE html>
  <html>
  <head>
    <title></title>
    <style>
      body {
        font-family: Helvetica;
        font-weight: 100;
        display: flex;
        justify-content: center;
      }
      input {
        padding: 0.5em;
        margin: 0.5em;
        font-size: 1em;
        border: 1px solid;
      }

      button {
        padding: 0.5em;
        font-size: 1em;
        margin: 0.5em;
        min-width: 3em;
        border: 1px solid;
        background-color: #eee;
      }
      #add-form {
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        align-items: center;
      }

      #items {
        list-style: none;
        margin: 0;
        padding: 0;
      }

      #items > li {
        display: flex;
        justify-content: space-between;
        align-items: center;
      }

      .container {
        width: 800px;
        display: flex;
        flex-direction: column;
      }

      #total {
        border-top: 1px solid;
        padding: 0.5em;
        margin-top: 0.5em;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <form id="add-form">
        <label>
          Name:
          <input id="name" type="text" placeholder="Item Name">
        </label>
        <label>
          Price:
          <input id="price" type="number" step="0.01" placeholder="Item Price">
        </label>
        <button id="add" type="submit">Add Item</button>
      </form>

      <ul id="items">
        <!-- Items here -->
      </ul>

      <div id="total">
        <!-- Total here -->
      </div>
    </div>
  
    <script>

      /*
      
      This example covers a wide range of JavaScript features. 

      - JS and DOM
      - Event Listeners 
      - variables 
      - functions 
      - if else conditionals and logic
      - Arrays 
      - Objects
      
      */


      document.querySelector('body').onclick = (e) => {
        console.log('---------------------------------')
        console.log(e.target)
      }

      const addForm = document.getElementById('add-form')
      const inputName = document.getElementById('name')
      const inputPrice = document.getElementById('price')
      const itemsList = document.getElementById('items')
      const divTotal = document.getElementById('total')

      const cart = []

      addForm.onsubmit = function(e) {
        e.preventDefault()
        const name = inputName.value
        const price = inputPrice.value
        
        addToCart(name, price)
        showCart()
      }

      itemsList.onclick = function(e) {
        console.log(e.target)
        if (e.target && e.target.classList.contains('remove')) {
          console.log(e.target.dataset.name)
          removeFromCart(e.target.dataset.name)
        } else if (e.target && e.target.classList.contains('add-one')) {
          addToCart(e.target.dataset.name)
        } else if (e.target && e.target.classList.contains('remove-one')) {
          removeFromCart(e.target.dataset.name, 1)
        }
      }

      itemsList.onchange = function(e) {
        if (e.target && e.target.classList.contains('update')) {
          const qty = parseInt(e.target.value)
          const name = e.target.dataset.name
          updateCart(name, qty)

        }
      }

      function addToCart(name, price) {
        for (let i = 0; i < cart.length; i += 1) {
          if (cart[i].name === name) {
            cart[i].qty += 1
            showCart()
            return true
          }
        }
        cart.push({ name, price, qty: 1})
        showCart()
      }

      function removeFromCart(name, qty = 0) {
        console.log(name, qty)
        for (let i = 0; i < cart.length; i += 1) {
          if (cart[i].name === name) {
            if (qty) {
              let newQty = cart[i].qty - qty
              if (newQty > 0) {
                cart[i].qty = newQty
              } else {
                cart.splice(i, 1)
              }
            } else {
              cart.splice(i, 1)
            }
          }
        }

        showCart()
      }

      function showCart() {
        let str = ''
        for (let i = 0; i < cart.length; i += 1) {
          str += `<li>
            <span>
              ${cart[i].name} ${cart[i].price} each 
              x ${cart[i].qty} = ${(cart[i].qty * cart[i].price).toFixed(2)}
            </span>
            <span>
              <button class="remove" data-name="${cart[i].name}">remove</button>
              <button class="add-one" data-name="${cart[i].name}"> + </button>
              <button class="remove-one" data-name="${cart[i].name}"> - </button>
              <input class="update" data-name="${cart[i].name}" type="number">
            </span>
          </li>`
        }
        itemsList.innerHTML = str
        divTotal.innerHTML = getTotal()
      }

      function getTotal() {
        let total = 0
        for (let i = 0; i < cart.length; i += 1) {
          total += cart[i].price * cart[i].qty
        }
        return total.toFixed(2)
      }

      function updateCart(name, qty) {
        for (let i = 0; i < cart.length; i += 1) {
          if (cart[i].name === name) {
            cart[i].qty = qty
            showCart()
            return true
          }
        }
        return false
      }

      // addToCart('Apple', .99)
      // addToCart('Apple', .99)
      // addToCart('Orange', 1.29)
      
      showCart()

      getTotal()

    </script>
  </body>
</html>
