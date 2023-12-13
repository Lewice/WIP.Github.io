<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Uwu Menu calculator</title>
  <script src="https://code.jquery.com/jquery-3.4.1.js" integrity="sha256-WpOohJOqMqqyKL9FccASB9O0KwACQJpFTUBLTYOVvVU=" crossorigin="anonymous"></script>
  <style>
    body, h2, form, label, p, button, select, input {
      font-size: 10;
      margin-right: 10px; /* Add a margin for spacing */
    }

    label {
      display: inline-block; /* Display as inline-block to make items appear beside each other */
      margin-bottom: 5px;
    }
    
    h3 {
  border: 1px solid black;
  padding: 5px;
}

    body, h2, form {
      text-align: center;
    }

    p {
      text-align: center;
      margin: 0; /* Remove default margin for <p> */
    }

    button {
      margin-top: 10px;
    }
	body {
	background-color: grey;
	}
  </style>
  <script>
  function calculateTotals() {
    // Reset totals and ingredients list
    document.getElementById('total').innerText = '';
    document.getElementById('commission').innerText = '';
    document.getElementById('ingredientsList').innerHTML = '';

    // Calculate total from selected items
    let total = 0;

    const menuItems = document.querySelectorAll('.menu-item:checked');
    menuItems.forEach(item => {
      const itemName = item.parentNode.textContent.trim();
      const price = parseFloat(item.dataset.price);
      const quantity = parseInt(item.nextElementSibling.value);
      const ingredients = calculateIngredients(itemName, quantity);

      if (!isNaN(price) && !isNaN(quantity) && quantity > 0) {
        // Exclude "Mystery Box" from discounts
        if (item.classList.contains('exclude-discount')) {
          total += price * quantity;
        } else {
          total += price * quantity * (1 - ($("#discount").val() / 100));
        }

        // Display ingredients for the selected item
        const ingredientsList = document.getElementById('ingredientsList');
        const listItem = document.createElement('li');
        listItem.textContent = `${quantity}x ${itemName} - Ingredients: ${ingredients.join(', ')}`;
        ingredientsList.appendChild(listItem);
      }
    });

    // Change commission rate from 5% to 10%
    const commission = total * 0.10;

    document.getElementById('total').innerText = total.toFixed(2);
    document.getElementById('commission').innerText = commission.toFixed(2);
  }

  function calculateIngredients(itemName, quantity) {
    if (itemName.includes('Choccy Pancakes')) {
      if (quantity >= 1 && quantity <= 6) {
        return ['3x Milk Canister', '3x Bag Of Sugar'];
      } else if (quantity >= 7 && quantity <= 12) {
        return ['6x Milk Canister', '6x Bag Of Sugar'];
      } else if (quantity >= 13 && quantity <= 18) {
        return ['9x Milk Canister', '9x Bag Of Sugar'];
      } else if (quantity >= 19 && quantity <= 24) {
        return ['12x Milk Canister', '12x Bag Of Sugar'];
      }
    } else if (itemName.includes('Apple Crumble')) {
      if (quantity >= 1 && quantity <= 3) {
        return ['3x Dough', '6x Bag Of Sugar'];
      } else if (quantity >= 4 && quantity <= 6) {
        return ['6x Dough', '12x Bag Of Sugar'];
      } else if (quantity >= 7 && quantity <= 9) {
        return ['9x Dough', '18x Bag Of Sugar'];
      } else if (quantity >= 10 && quantity <= 12) {
        return ['12x Dough', '24x Bag Of Sugar'];
      }
    } else if (itemName.includes('Salad')) {
	 if (quantity >= 1 && quantity <= 5) {
		return ['2x Lettuce', '3x Cucumber', '5x Peas', '3x Tomatoes'];
	 } else if (quantity >= 6 && quantity <= 10) {
		return ['4x Lettuce', '6x Cucumber', '10x Peas', '6x Tomatoes'];
	 } else if (quantity >= 11 && quantity <= 15) {
		return ['6x Lettuce', '9x Cucumber', '15x Peas', '9x Tomatoes'];
	 } else if (quantity >= 20 && quantity <= 25) {
		return ['8x Lettuce', '12x Cucumber', '20x Peas', '12x Tomatoes'];
     }
	} else if (itemName.includes('Fruit Explosion')) {
	 if (quantity >= 1 && quantity <= 4) {
		return ['1x Plastic Cup', '1x Milk Canister', '8x Bag Of Sugar', '10x Oranges'];
	 } else if (quantity >= 5 && quantity <= 8) {
		return ['2x Plastic Cup', '2x Milk Canister', '16x Bag Of Sugar', '20x Oranges'];
	 } else if (quantity >= 9 && quantity <= 12) {
		return ['3x Plastic Cup', '3x Milk Canister', '24x Bag Of Sugar', '30x Oranges'];
	 } else if (quantity >= 13 && quantity <= 16) {
		return ['4x Plastic Cup', '4x Milk Canister', '32x Bag Of Sugar', '40x Oranges'];
	}
	} else if (itemName.includes('Homemade Cat Cookies')) {
	 if (quantity >= 1 && quantity <= 12) {
		return ['1x Dough', '2x Bag Of Sugar', '1x Icing'];
	 } else if (quantity >= 13 && quantity <= 24) {
		return ['2x Dough', '4x Bag Of Sugar', '2x Icing'];
	 } else if (quantity >= 25 && quantity <= 36) {
		return ['3x Dough', '6x Bag Of Sugar', '3x Icing'];
	 } else if (quantity >= 37 && quantity <= 48) {
		return ['4x Dough', '8x Bag Of Sugar', '4x Icing'];
	 }
	} else if (itemName.includes('Cat Cupcake')) {
	 if (quantity >= 1 && quantity <= 6) {
		return ['2x Dough', '2x Bag Of Sugar', '4x Icing'];
	 } else if (quantity >= 7 && quantity <= 12) {
		return ['4x Dough', '4x Bag Of Sugar', '8x Icing'];
	 } else if (quantity >= 13 && quantity <= 18) {
		return ['6x Dough', '6x Bag Of Sugar', '12x Icing'];
	 } else if (quantity >= 19 && quantity <= 24) {
		return ['8x Dough', '8x Bag Of Sugar', '16x Icing'];
	 }
	} else if (itemName.includes('Frozen Yoghurt')) {
	 if (quantity >= 1 && quantity <= 4) {
		return ['1x Plastic Cup', '1x Milk Canister', '1x Bag Of Sugar'];
	 } else if (quantity >= 5 && quantity <= 8) {
		return ['2x Plastic Cup', '2x Milk Canister', '2x Bag Of Sugar'];
	 } else if (quantity >= 9 && quantity <= 12) {
		return ['3x Plastic Cup', '3x Milk Canister', '3x Bag Of Sugar'];
	 } else if (quantity >= 13 && quantity <= 16) {
		return ['4x Plastic Cup', '4x Milk Canister', '4x Bag Of Sugar'];
	}
	} else if (itemName.includes('Fresh Lemonade')) {
	 if (quantity >= 1 && quantity <= 5) {
		return ['5x Plastic Cup', '15x Orange'];
	 } else if (quantity >= 6 && quantity <= 10) {
		return ['10x Plastic Cup', '30x Orange'];
	 } else if (quantity >= 11 && quantity <= 15) {
		return ['15x Plastic Cup', '45x Orange'];
	 } else if (quantity >= 16 && quantity <= 20) {
		return ['20x Plastic Cup', '60x Orange'];
	}
	} else if (itemName.includes('Iced Coffee')) {
	 if (quantity >= 1 && quantity <= 5) {
		return ['1x Plastic Cup', '1x Coffee Beans', '1x Milk Canister'];
	 } else if (quantity >= 6 && quantity <= 10) {
		return ['2x Plastic Cup', '2x Coffee Beans', '2x Milk Canister'];
	 } else if (quantity >= 11 && quantity <= 15) {
		return ['3x Plastic Cup', '3x Coffee Beans', '3x Milk Canister'];
	 } else if (quantity >= 16 && quantity <= 20) {
		return ['4x Plastic Cup', '4x Coffee Beans', '4x Milk Canister'];
	}
	} else if (itemName.includes('Matcha Latte')) {
	 if (quantity >= 1 && quantity <= 5) {
		return ['1x Plastic Cup', '2x Tea Leaf', '1x Milk Canister'];
	 } else if (quantity >= 6 && quantity <= 10) {
		return ['2x Plastic Cup', '4x Tea Leaf', '2x Milk Canister'];
	 } else if (quantity >= 11 && quantity <= 15) {
		return ['3x Plastic Cup', '6x Tea Leaf', '3x Milk Canister'];
	 } else if (quantity >= 16 && quantity <= 20) {
		return ['4x Plastic Cup', '8x Tea Leaf', '4x Milk Canister'];
	}
	} else if (itemName.includes('Pumpkin Spice Latte')) {
	 if (quantity >= 1 && quantity <= 5) {
		return ['1x Plastic Cup', '3x Coffee Beans', '1x Milk Canister'];
	 } else if (quantity >= 6 && quantity <= 10) {
		return ['2x Plastic Cup', '6x Coffee Beans', '2x Milk Canister'];
	 } else if (quantity >= 11 && quantity <= 15) {
		return ['3x Plastic Cup', '9x Coffee Beans', '3x Milk Canister'];
	 } else if (quantity >= 16 && quantity <= 20) {
		return ['4x Plastic Cup', '12x Coffee Beans', '4x Milk Canister'];
	}
	} else if (itemName.includes('Cat Tuccino')) {
	 if (quantity >= 1 && quantity <= 3) {
		return ['1x Plastic Cup', '3x Coffee Beans', '1x Milk Canister'];
	 } else if (quantity >= 4 && quantity <= 6) {
		return ['2x Plastic Cup', '6x Coffee Beans', '2x Milk Canister'];
	 } else if (quantity >= 7 && quantity <= 9) {
		return ['3x Plastic Cup', '9x Coffee Beans', '3x Milk Canister'];
	 } else if (quantity >= 10 && quantity <= 12) {
		return ['4x Plastic Cup', '12x Coffee Beans', '4x Milk Canister'];
	}
	} else if (itemName.includes('Bobba Tea')) {
	 if (quantity >= 1 && quantity <= 5) {
		return ['1x Plastic Cup', '2x Tea Leaf'];
	 } else if (quantity >= 6 && quantity <= 10) {
		return ['2x Plastic Cup', '4x Tea Leaf'];
	 } else if (quantity >= 11 && quantity <= 15) {
		return ['3x Plastic Cup', '6x Tea Leaf'];
	 } else if (quantity >= 16 && quantity <= 20) {
		return ['4x Plastic Cup', '8x Tea Leaf'];
	}
	} else if (itemName.includes('Green Tea')) {
	 if (quantity >= 1 && quantity <= 5) {
		return ['1x Plastic Cup', '4x Tea Leaf'];
	 } else if (quantity >= 6 && quantity <= 10) {
		return ['2x Plastic Cup', '8x Tea Leaf'];
	 } else if (quantity >= 11 && quantity <= 15) {
		return ['3x Plastic Cup', '12x Tea Leaf'];
	 } else if (quantity >= 16 && quantity <= 20) {
		return ['4x Plastic Cup', '16x Tea Leaf'];
	}
	} else if (itemName.includes('Cat Donut')) {
	 if (quantity >= 1 && quantity <= 6) {
		return ['2x Dough', '2x Bag Of Sugar', '2x Icing'];
	 } else if (quantity >= 7 && quantity <= 12) {
		return ['4x Dough', '4x Bag Of Sugar', '4x Icing'];
	 } else if (quantity >= 13 && quantity <= 18) {
		return ['6x Dough', '6x Bag Of Sugar', '6x Icing'];
	 } else if (quantity >= 19 && quantity <= 24) {
		return ['8x Dough', '8x Bag Of Sugar', '8x Icing'];
	}
	}

    // Default ingredients for other items
    return ['Default Ingredient 1', 'Default Ingredient 2', 'Default Ingredient 3'];
  }

    function SubForm() {
      // Check if the employee name is provided
      const employeeName = $("#employeeName").val();
      if (employeeName.trim() === "") {
        alert("Employee Name is required!");
        return;
      }

      // Get the total from the UI
      const totalText = $("#total").text();
      const total = parseFloat(totalText);

      // Check if the total is a valid number
      if (isNaN(total)) {
        alert("Total is not available. Please calculate totals first.");
        return;
      }

      // Get selected menu items and quantities
      const orderedItems = [];
      const menuItems = document.querySelectorAll('.menu-item:checked');
      menuItems.forEach(item => {
        const itemName = item.parentNode.textContent.trim();
        const price = parseFloat(item.dataset.price);
        const quantity = parseInt(item.nextElementSibling.value);

        if (!isNaN(price) && !isNaN(quantity) && quantity > 0) {
          orderedItems.push({
            name: itemName,
            price: price,
            quantity: quantity
          });
        }
      });

      // Calculate total and commission
      const commission = total * 0.10;

      // Prepare data for API submission
      const formData = {
        "Employee Name": employeeName,
        "Total": total.toFixed(2),
        "Commission": commission.toFixed(2),
        "Items Ordered": JSON.stringify(orderedItems),
        "Discount Applied": parseFloat($("#discount").val())
      };

      // Form Submission Logic for Spreadsheet
      $.ajax({
        url: "https://api.apispreadsheets.com/data/wy0vT9JJYGL6a8IZ/",
        type: "post",
        data: formData,
        headers: {
          accessKey: "c9d38abe3a9ed79cd6f8d878d8986f6f",
          secretKey: "fb1fe402814e22e7a92cb48ce0937cb0",
          "Content-Type": "application/x-www-form-urlencoded",
        },
        success: function () {
          alert("Form Data Submitted to Spreadsheet and Discord :)");
          resetForm();
        },
        error: function () {
          alert("There was an error :(");
        }
      });

      // Prepare data for Discord webhook
      const discordData = {
        username: "Menu Order Bot",
        content: `New order submitted by ${employeeName}`,
        embeds: [{
          title: "Order Details",
          fields: [
            { name: "Employee Name", value: employeeName, inline: true },
            { name: "Total", value: `$${total.toFixed(2)}`, inline: true },
            { name: "Commission", value: `$${commission.toFixed(2)}`, inline: true },
            { name: "Discount Applied", value: `${formData["Discount Applied"]}%`, inline: true },
            { name: "Items Ordered", value: orderedItems.map(item => `${item.quantity}x ${item.name}`).join('\n') }
          ],
          color: 0x00ff00 // You can customize the color
        }]
      };

      // Form Submission Logic for Discord webhook
      $.ajax({
        url: "https://discord.com/api/webhooks/1157451563212750959/FqNuldbbd1b4cZOxmo3xsbngVnMEWZfOSyXxwtwMuv7iTmeLhgDbL6maZiZJnfgYgVwy",
        type: "post",
        contentType: "application/json",
        data: JSON.stringify(discordData),
        success: function () {
          // Do nothing specific for Discord success
        },
        error: function () {
          console.error("Error sending data to Discord :(");
        }
      });
    }

    function resetForm() {
      // Reset checkboxes and quantity inputs
      $('.menu-item').prop('checked', false);
      $('.quantity').val(1);

      // Reset totals
      document.getElementById('total').innerText = '';
      document.getElementById('commission').innerText = '';

      // Clear ingredients list
      document.getElementById('ingredientsList').innerHTML = '';

      // Reset discount dropdown to default
      $("#discount").val("0");
    }
  </script>
</head>
<body>

  <h2>Uwu Menu</h2>
<a href="NewMenu.html">Produce Calculator</a>

  <form id="menuForm">
  <h3>Specials</h3>
    <label>
      <input type="checkbox" class="menu-item" data-price="1500" data-ingredients="5 Cattacinos/iced coffee, 5 Choccy Pancakes, 5 Homemade Cat Cookies"> Uwu Daddy Special - $1500
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="1500" data-ingredients="5 Bobba Tea's, 5 Extra Beefy Sammies, 5 Donut/Cupcakes"> Uwu Mommy Special - $1500
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="250" data-ingredients="Turkey Sandwhich, Pumpkin Spice Latte, Apple Crumble"> Basic Bitch Special - $250
      <input type="number" class="quantity" value="1" min="1">
    </label>
	
	<h3>Specials</h3>
    <label>
      <input type="checkbox" class="menu-item" data-price="300" data-ingredients="Choccy Pancakes, Pumpkin Spice Latte, Cat Cookie/Donut"> Colin's Choice - $300
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="300" data-ingredients="Salad/Turkey Sandwhich, Matcha Latte, Apple Crumble"> Judy's Choice - $300
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="300" data-ingredients="BLT/Turkey Sandwhich, Bobba Tea, Cat Cookie/Donut"> Velma's Choice - $300
      <input type="number" class="quantity" value="1" min="1">
    </label>
	<label>
      <input type="checkbox" class="menu-item" data-price="300" data-ingredients="Salad/Turkey Sandwhich, Matcha Latte, Cat Cookie/Donut"> Dave's Choice - $300
      <input type="number" class="quantity" value="1" min="1">
    </label>
	
	<h3>Entree</h3>
    <label>
      <input type="checkbox" class="menu-item" data-price="150" data-ingredients="2x Lettuce,3x Cucumber, 5x Peas, 3x Tomatoes"> Salad - $150
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="200" data-ingredients="1x Plastic Cup, 1x Milk Canister,8x Bag Of Sugar, 10x Oranges"> Fruit Explosion - $200
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="150" data-ingredients="1x Bread, 1x Meat device"> Sandwhiches - $150
      <input type="number" class="quantity" value="1" min="1">
    </label>
	<label>
      <input type="checkbox" class="menu-item" data-price="175" data-ingredients="3x Milk Canister, 3x Bag Of Sugar"> Choccy Pancakes - $175
      <input type="number" class="quantity" value="1" min="1">
    </label>
	
	<h3>Desserts</h3>
    <label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="1x Dough, 2x Bag Of Sugar, 1x Icing"> Homemade Cat Cookies - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="3x Dough,6x Bag Of Sugar"> Apple Crumble - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="2x Dough, 2x Bag of Sugar, 2x Icing"> Cat Donut - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
	<label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="2x Dough ,2x Bag Of Sugar , 2x Icing"> Cat Cupcake - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
	
	<h3>Delivery</h3>
    <label>
      <input type="checkbox" class="menu-item" data-price="250" data-ingredients="1x City Delivery"> City Delivery - $250
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="500" data-ingredients="1x Sandy Delivery"> Sandy Delivery - $500
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="750" data-ingredients="1x Poleto Delivery"> Poleto Delivery - $750
      <input type="number" class="quantity" value="1" min="1">
    </label>
	
	<h3>Misc Items</h3>
    <label>
      <input type="checkbox" class="menu-item exclude-discount" data-price="5000" data-ingredients="1x Mystery Box"> Mystery Box - $5000
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="2500" data-ingredients="1x Box"> Box's - $2500
      <input type="number" class="quantity" value="1" min="1">
    </label>
	
	<h3>Cattacino Specials</h3>
    <label>
      <input type="checkbox" class="menu-item" data-price="1600" data-ingredients="10x Cattacinos"> 10 for 1600$ 
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="2500" data-ingredients="20x Cattacinos"> 20 for 2500$
      <input type="number" class="quantity" value="1" min="1">
    </label>
	<label>
      <input type="checkbox" class="menu-item" data-price="3500" data-ingredients="30x Cattacinos"> 30 for 3500$
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="4500" data-ingredients="40x Cattacinos"> 40 for 4500$
      <input type="number" class="quantity" value="1" min="1">
    </label>
	<label>
      <input type="checkbox" class="menu-item" data-price="5500" data-ingredients="50x Cattacinos"> 50 for 5500$
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="9000" data-ingredients="100x Cattacinos"> 100 for 9000$
      <input type="number" class="quantity" value="1" min="1">
    </label>
	
	<h3>Beverages</h3>
    <label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="1x Plastic Cup, 1x Milk Canister, 1x Bag Of Sugar"> Frozen Yoghurt - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="200" data-ingredients="5x Plastic Cup, 15x Orange "> Fresh Lemonade - $200
      <input type="number" class="quantity" value="1" min="1">
    </label>
	<label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="1x Plastic Cup, 1x Coffee Beans, 1x Milk Canister"> Iced Coffee - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="1x Plastic Cup, 2x Tea Leaf, 1x Milk Canister"> Matcha Latte - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
	<label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="1x Platic Cup, 1x Coffee Beans, 1x Milk Canister"> Pumpkin Spice Latte - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="200" data-ingredients="1x Plastic Cup, 3x Coffee Beans, 1x Milk Canister"> Cat Tuccino - $200
      <input type="number" class="quantity" value="1" min="1">
    </label>
	<label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="1x Plastic Cup, 2x Tea Leaf"> Bobba Tea - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
    <label>
      <input type="checkbox" class="menu-item" data-price="125" data-ingredients="1x Plastic Cup, 4x Tea Leaf"> Green Tea - $125
      <input type="number" class="quantity" value="1" min="1">
    </label>
	

	
	
	
	
	
	<div style="margin-bottom: 30px;"></div>
	
	<label for="discount">Select Discount:</label>
    <select id="discount" onchange="calculateTotals()">
      <option value="0">No Discount</option>
      <option value="25">25% Discount</option>
      <option value="30">30% Discount</option>
      <option value="50">50% Discount</option>
    </select>
	
	<div style="margin-bottom: 30px;"></div>
	


    <label for="employeeName">Employee Name:</label>
    <input type="text" id="employeeName" required>
	
	<div style="margin-bottom: 30px;"></div>
	
	

    <p>Total: $<span id="total"></span></p>
    <p>Commission (10%): $<span id="commission"></span></p>
	<div id="ingredients">
	<h3>Ingredients Needed</h3>
	<ul id="ingredientsList"></ul>
	</div>
	
	<div style="margin-bottom: 30px;"></div>

    <button type="button" onclick="calculateTotals()">Calculate</button>
    <button type="button" onclick="SubForm()">Submit</button>
    <button type="button" onclick="resetForm()">Reset</button>
  </form>

</body>
</html>
