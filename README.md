# Resturant-chatbox
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spice Garden Restaurant</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .chat-button {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 70px;
            height: 70px;
            background: linear-gradient(135deg, #ff6b35, #f7931e);
            border-radius: 50%;
            border: none;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            transition: all 0.3s ease;
            animation: pulse 2s infinite;
            z-index: 1000;
            font-size: 35px;
        }

        .chat-button:hover {
            transform: scale(1.1);
        }

        @keyframes pulse {
            0%, 100% {
                box-shadow: 0 10px 30px rgba(255, 107, 53, 0.4);
            }
            50% {
                box-shadow: 0 10px 40px rgba(255, 107, 53, 0.8);
            }
        }

        .chat-container {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 900px;
            max-width: 90vw;
            height: 700px;
            max-height: 90vh;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            display: none;
            flex-direction: column;
            overflow: hidden;
            z-index: 1000;
        }

        .chat-container.active {
            display: flex;

            animation: slideUp 0.4s ease-out;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(50px) scale(0.9);
            }
            to {
                opacity: 1;
                transform: translateY(0) scale(1);
            }
        }

        .chat-header {
            background: linear-gradient(135deg, #ff6b35, #f7931e);
            padding: 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            color: white;
        }

        .chat-header-content {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .sparkle {
            font-size: 30px;
            animation: rotate 3s linear infinite;
        }

        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .chat-title h2 {
            font-size: 24px;
            font-weight: bold;
            margin: 0;
        }

        .chat-title p {
            font-size: 13px;
            opacity: 0.9;
            margin: 0;
        }

        .header-right {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .cart-button {
            position: relative;
            background: rgba(255, 255, 255, 0.2);
            border: none;
            padding: 10px 20px;
            border-radius: 25px;
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 14px;
        }

        .cart-button:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .cart-count {
            position: absolute;
            top: -8px;
            right: -8px;
            background: #ef4444;
            color: white;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            font-weight: bold;
        }

        .close-btn {
            width: 40px;
            height: 40px;
            background: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 50%;
            cursor: pointer;
            font-size: 24px;
            color: white;
            transition: all 0.3s ease;
        }

        .close-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: rotate(90deg);
        }

        .category-buttons {
            display: none;
            gap: 10px;
            padding: 15px;
            background: linear-gradient(135deg, #fff5f0, #ffe8dc);
            border-bottom: 2px solid #f0f0f0;
        }

        .category-buttons.show {
            display: flex;
            animation: slideDown 0.5s ease-out;
        }

        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .category-btn {
            flex: 1;
            padding: 15px;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            color: white;
        }

        .category-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
        }

        .category-btn.veg {
            background: #10b981;
        }

        .category-btn.nonveg {
            background: #ef4444;
        }

        .category-btn.beverages {
            background: #3b82f6;
        }

        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            background: #f9fafb;
        }

        .message {
            margin-bottom: 15px;
            display: flex;
            animation: messageSlide 0.4s ease-out;
        }

        @keyframes messageSlide {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .message.bot {
            justify-content: flex-start;
        }

        .message.user {
            justify-content: flex-end;
        }

        .message-content {
            max-width: 70%;
            padding: 12px 18px;
            border-radius: 18px;
            word-wrap: break-word;
        }

        .message.bot .message-content {
            background: white;
            color: #333;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        }

        .message.user .message-content {
            background: linear-gradient(135deg, #ff6b35, #f7931e);
            color: white;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-top: 20px;
        }

        .menu-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
        }

        .menu-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.2);
        }

        .menu-card-image-container {
            position: relative;
            overflow: hidden;
            height: 180px;
        }

        .menu-card-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.5s ease;
        }

        .menu-card:hover .menu-card-image {
            transform: scale(1.1);
        }

        .menu-card-price {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #ff6b35;
            color: white;
            padding: 6px 12px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 14px;
        }

        .menu-card-body {
            padding: 15px;
        }

        .menu-card-title {
            font-size: 18px;
            font-weight: bold;
            color: #333;
            margin-bottom: 8px;
        }

        .menu-card-description {
            font-size: 13px;
            color: #666;
            margin-bottom: 12px;
            line-height: 1.4;
        }

        .menu-card-footer {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 10px;
        }

        .menu-card-badge {
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 600;
        }

        .spice-badge {
            background: #fee2e2;
            color: #dc2626;
        }

        .type-badge {
            background: #dbeafe;
            color: #2563eb;
        }

        .order-btn {
            background: #ff6b35;
            color: white;
            border: none;
            padding: 6px 16px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .order-btn:hover {
            background: #f7931e;
            transform: scale(1.05);
        }

        .cart-summary {
            background: white;
            border-radius: 15px;
            padding: 20px;
            margin-top: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            animation: cardAppear 0.5s ease-out;
        }

        @keyframes cardAppear {
            from {
                opacity: 0;
                transform: scale(0.9);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        .cart-summary h3 {
            color: #ff6b35;
            margin-bottom: 15px;
            font-size: 20px;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 0;
            border-bottom: 1px solid #f0f0f0;
        }

        .cart-item-info {
            display: flex;
            align-items: center;
            gap: 10px;
            flex: 1;
        }

        .cart-item-name {
            font-weight: 600;
            color: #333;
        }

        .cart-item-qty {
            background: #f0f0f0;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 12px;
            color: #666;
        }

        .cart-item-price {
            font-weight: bold;
            color: #ff6b35;
            margin-right: 10px;
        }

        .cart-item-remove {
            background: #ef4444;
            color: white;
            border: none;
            padding: 4px 10px;
            border-radius: 12px;
            font-size: 11px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .cart-item-remove:hover {
            background: #dc2626;
        }

        .cart-total {
            margin-top: 15px;
            padding-top: 15px;
            border-top: 2px solid #ff6b35;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .cart-total-label {
            font-size: 18px;
            font-weight: bold;
            color: #333;
        }

        .cart-total-amount {
            font-size: 24px;
            font-weight: bold;
            color: #ff6b35;
        }

        .checkout-btn {
            width: 100%;
            margin-top: 15px;
            padding: 15px;
            background: linear-gradient(135deg, #10b981, #059669);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .checkout-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(16, 185, 129, 0.4);
        }

        .chat-input-container {
            padding: 15px;
            background: white;
            border-top: 2px solid #f0f0f0;
            display: flex;
            gap: 10px;
        }

        .chat-input {
            flex: 1;
            padding: 12px 18px;
            border: 2px solid #e5e7eb;
            border-radius: 25px;
            font-size: 14px;
            outline: none;
            transition: border-color 0.3s ease;
        }

        .chat-input:focus {
            border-color: #ff6b35;
        }

        .send-btn {
            background: linear-gradient(135deg, #ff6b35, #f7931e);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 18px;
            transition: all 0.3s ease;
        }

        .send-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 15px rgba(255, 107, 53, 0.4);
        }

        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }

        ::-webkit-scrollbar-thumb {
            background: #ff6b35;
            border-radius: 4px;
        }
    
    </style>
     <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Animated Contact Form</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #1e3c72, #2a5298);
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
      overflow: hidden;
    }

    /* Floating glowing animation background */
    .animated-bg {
      position: absolute;
      width: 200px;
      height: 200px;
      border-radius: 50%;
      background: rgba(255,255,255,0.15);
      animation: float 6s infinite ease-in-out alternate;
    }

    .animated-bg:nth-child(1) {
      top: 10%;
      left: 15%;
      animation-delay: 0s;
    }

    .animated-bg:nth-child(2) {
      bottom: 15%;
      right: 10%;
      animation-delay: 2s;
    }

    .animated-bg:nth-child(3) {
      top: 50%;
      right: 25%;
      animation-delay: 4s;
    }

    @keyframes float {
      0% { transform: translateY(0) scale(1); }
      100% { transform: translateY(-30px) scale(1.1); }
    }

    .form-container {
      position: relative;
      background: #ffffff;
      padding: 35px 40px;
      border-radius: 20px;
      width: 100%;
      max-width: 420px;
      box-shadow: 0 12px 30px rgba(0,0,0,0.25);
      animation: fadeIn 1s ease-in-out;
      border: 3px solid transparent;
      background-clip: padding-box;
    }

    .form-container:before {
      content: "";
      position: absolute;
      top: -3px; left: -3px; right: -3px; bottom: -3px;
      border-radius: 20px;
      background: linear-gradient(135deg, #ff00cc, #57579b, #00c6ff);
      background-size: 300% 300%;
      z-index: -1;
      animation: borderMove 6s linear infinite;
    }

    @keyframes borderMove {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    .form-container h2 {
      text-align: center;
      margin-bottom: 25px;
      color: #333;
      font-size: 24px;
      position: relative;
    }

    .form-container h2::after {
      content: "";
      width: 50px;
      height: 3px;
      background: linear-gradient(90deg, #ff00cc, #333399);
      display: block;
      margin: 8px auto 0;
      border-radius: 2px;
    }

    label {
      display: block;
      margin-bottom: 8px;
      font-weight: 600;
      color: #444;
      font-size: 14px;
    }

    input, textarea {
      width: 100%;
      padding: 12px;
      margin-bottom: 20px;
      border: 2px solid #ccc;
      border-radius: 10px;
      font-size: 15px;
      transition: all 0.3s ease;
    }

    input:focus, textarea:focus {
      border-color: #6a11cb;
      box-shadow: 0 0 12px rgba(106, 17, 203, 0.3);
      outline: none;
      transform: scale(1.02);
    }

    textarea {
      resize: none;
      height: 120px;
    }

    button {
      width: 100%;
      padding: 14px;
      background: linear-gradient(135deg, #6a11cb, #2575fc);
      border: none;
      border-radius: 10px;
      font-size: 16px;
      font-weight: bold;
      color: #fff;
      cursor: pointer;
      transition: all 0.3s ease;
      position: relative;
      overflow: hidden;
    }

    button::before {
      content: "";
      position: absolute;
      top: 0; left: -100%;
      width: 100%; height: 100%;
      background: rgba(255,255,255,0.3);
      transform: skewX(-20deg);
      transition: 0.5s;
    }

    button:hover::before {
      left: 100%;
    }

    button:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 8px 20px rgba(37, 117, 252, 0.3);
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
    
  <!-- Floating glowing background elements -->
  <div class="animated-bg"></div>
  <div class="animated-bg"></div>
  <div class="animated-bg"></div>

  <div class="form-container">
    <h2>Contact Us</h2>
   <!-- modify this form HTML and place wherever you want your form -->
<form
  action="https://formspree.io/f/mwprbojo"
  method="POST"
>
  <label>
    Your email:
    <input type="email" name="email">
  </label>
  <label>
    Your Review:
    <textarea name="message"></textarea>
  </label>
  <!-- your other form fields go here -->
  <button type="submit">Send</button>
</form>
  </div>
</body>
</html>

    
    
</head>
<body>
    <button class="chat-button" id="chatButton">💬</button>

    <div class="chat-container" id="chatContainer">
        <div class="chat-header">
            <div class="chat-header-content">
                <span class="sparkle">✨</span>
                <div class="chat-title">
                    <h2>Spice Garden</h2>
                    <p>Authentic Indian Cuisine</p>
                </div>
            </div>
            <div class="header-right">
                <button class="cart-button" id="viewCartBtn">
                    🛒 Cart
                    <span class="cart-count" id="cartCount">0</span>
                </button>
                <button class="close-btn" id="closeBtn">×</button>
            </div>
        </div>

        <div class="category-buttons" id="categoryButtons">
            <button class="category-btn veg" data-category="veg">🥗 Vegetarian</button>
            <button class="category-btn nonveg" data-category="nonveg">🍗 Non-Veg</button>
            <button class="category-btn beverages" data-category="beverages">🥤 Beverages</button>
        </div>

        <div class="chat-messages" id="chatMessages"></div>

        <div class="chat-input-container">
            <input type="text" class="chat-input" id="chatInput" placeholder="Ask me anything about our menu...">
            <button class="send-btn" id="sendBtn">➤</button>
        </div>
    </div>
    <section id="about" class="about">
    <div class="about-grid" style="display:flex; flex-direction:column; align-items:center; gap:15px;">

        

        <section id="about" class="about">
    <div class="about-grid" style="display:flex; flex-direction:column; align-items:center; gap:20px; text-align:center;">

        <!-- Image with inline styling -->
        <div class="about-image-container">
            <div class="image-frame" 
                 style="width:230px; height:230px; overflow:hidden; border-radius:50%; box-shadow:0px 6px 20px rgba(0,0,0,0.3); transition: transform 0.3s ease; margin:auto;">
                <img src="image.jpg" alt="Adarsh Kumar" class="profile-image"
                     style="width:100%; height:100%; object-fit:cover; border-radius:50%; transition: transform 0.3s ease;"
                     onmouseover="this.style.transform='scale(1.1)'" 
                     onmouseout="this.style.transform='scale(1)'">
            </div>
        </div>

        <!-- Floating Badges -->
        <div class="floating-badge badge-1" 
             style="display:flex; align-items:center; gap:8px; background:#4CAF50; color:#fff; padding:8px 16px; border-radius:20px; font-size:17px; font-weight:500; box-shadow:0px 3px 10px rgba(0, 0, 0, 0.2); animation: float 2s infinite alternate;">
            <div class="badge-icon">
                <i class="fas fa-code"></i>
            </div>
            <div class="badge-text"> Welcome to</div>
        </div>

        <div class="floating-badge badge-2" 
             style="display:flex; align-items:center; gap:8px; background:#2196F3; color:#fff; padding:8px 16px; border-radius:20px; font: size 22px; font-weight:500; box-shadow:0px 3px 10px rgba(0, 0, 0, 0.625); animation: float 3s infinite alternate;">
            <div class="badge-icon">
                <i class="fas fa-graduation-cap"></i>
            </div>
            <div class="badge-text">Spice Garden</div>
        </div>
    </div>

    <!-- Inline Keyframe Animation -->
    <style>
        @keyframes float {
            from { transform: translateY(0px); }
            to { transform: translateY(-10px); }
        }
    </style>
</section>


    <script>
        const menuData = {
            veg: [
                { name: "Indian Curry", price: 12.99, description: "Rich and flavorful curry with aromatic spices", image: "indian curry.W0fhHHdQW5JCm_HeM7wMwgHaE8", spice: "Medium" },
                { name: "Mixed Vegetables", price: 9.99, description: "Colorful mixed vegetables in savory sauce", image: "Cook-Mixed-Vegetables-Step-19-3165735289.jpg", spice: "Mild" },
                { name: "Vegetable Biryani", price: 11.99, description: "Fragrant basmati rice with mixed vegetables", image: "https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?w=400&h=300&fit=crop", spice: "Medium" },
                { name: "Green Curry", price: 11.49, description: "Creamy green vegetable curry with herbs", image: "vegan-green-curry-sq-1-2370522378.jpg", spice: "Mild" },
                { name: "Spicy Vegetable Stew", price: 9.49, description: "Hearty vegetable stew in tomato gravy", image: "veg strew.r-MUyLfr6fo05wxk_ObdTAHaFz", spice: "Medium" },
                { name: "Grilled Mushrooms", price: 10.99, description: "Fresh grilled mushrooms with herbs", image: "grilled mashroom.-4fngLj5t8ckCvIpqW9O0gHaEK", spice: "Medium" },
                { name: "Vegetable Stir Fry", price: 10.49, description: "Indo-Chinese style vegetable stir fry", image: "veg stir fry.cBd8WwlTbdAg-pPDwhRZ2QHaLH", spice: "Hot" },
                { name: "Mixed Veggie Bowl", price: 8.99, description: "Healthy bowl with fresh mixed vegetables", image: "https://images.unsplash.com/photo-1505253758473-96b7015fcd40?w=400&h=300&fit=crop", spice: "Mild" }
            ],
            nonveg: [
                { name: "Butter Chicken", price: 14.99, description: "Tender chicken in creamy tomato sauce", image: "https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?w=400&h=300&fit=crop", spice: "Medium" },
                { name: "Chicken Biryani", price: 13.99, description: "Aromatic rice layered with succulent chicken", image: "https://images.unsplash.com/photo-1563379091339-03b21ab4a4f8?w=400&h=300&fit=crop", spice: "Hot" },
                { name: "Spicy Curry", price: 16.99, description: "Rich and spicy curry with tender meat", image: "https://images.unsplash.com/photo-1585937421612-70a008356fbe?w=400&h=300&fit=crop", spice: "Hot" },
                { name: "Chicken Tikka", price: 12.99, description: "Chargrilled chicken chunks with spices", image: "https://images.unsplash.com/photo-1599487488170-d11ec9c172f0?w=400&h=300&fit=crop", spice: "Medium" },
                { name: "Fish Curry", price: 15.49, description: "Fresh fish in coconut curry sauce", image: "fish curry.WfUXLo8DaHhrp5B-pBNYPgHaE7", spice: "Medium" },
                { name: "Tandoori Chicken", price: 13.49, description: "Clay oven roasted marinated chicken", image: "https://images.unsplash.com/photo-1610057099443-fde8c4d50f91?w=400&h=300&fit=crop", spice: "Hot" },
                { name: "Chicken Korma", price: 14.49, description: "Mild creamy chicken in almond sauce", image: "CHIC+KORMA+FIVE-364818462.jpg", spice: "Mild" },
                { name: "Naan and chicken curry", price: 17.99, description: "Fresh chicken curry  in spicy gravy", image: "https://images.unsplash.com/photo-1565557623262-b51c2513a641?w=400&h=300&fit=crop", spice: "Hot" },
                { name: "Meat Curry", price: 15.99, description: "Tender meat cooked with aromatic spices", image: "https://images.unsplash.com/photo-1574484284002-952d92456975?w=400&h=300&fit=crop", spice: "Medium" },
                { name: "Chicken Curry", price: 13.99, description: "Classic chicken curry with rich gravy", image: "chicken curry.nTT5tvHk0Up59zRcC6oEygHaHa", spice: "Medium" }
            ],
            beverages: [
                { name: "Mango Lassi", price: 4.99, description: "Refreshing yogurt drink with mango", image: "https://images.unsplash.com/photo-1623065422902-30a2d299bbe4?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Masala Chai", price: 3.99, description: "Traditional spiced tea with milk", image: "https://images.unsplash.com/photo-1571934811356-5cc061b6821f?w=400&h=300&fit=crop", type: "Hot" },
                { name: "Lime Drink", price: 3.49, description: "Refreshing lime beverage", image: "line drink.jpg", type: "Cold" },
                { name: "Sweet Lassi", price: 4.49, description: "Classic sweet yogurt drink", image: "sweet lassi.I9ihXCNpFsYrHh6-e65vIQHaFj", type: "Cold" },
                { name: "Cola", price: 2.99, description: "Classic cola served chilled", image: "https://images.unsplash.com/photo-1554866585-cd94860890b7?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Sprite", price: 2.99, description: " Classic served chilled soda", image: "https://images.unsplash.com/photo-1625772299848-391b6a87d7b3?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Orange Drink", price: 2.99, description: "Orange flavored beverage", image: "https://images.unsplash.com/photo-1581636625402-29b2a704ef13?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Pepsi", price: 2.99, description: " Energy beverage", image: "https://images.unsplash.com/photo-1629203851122-3726ecdf080e?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Iced Tea", price: 3.49, description: "Chilled tea with lemon", image: "ice tea.IOJxhN1oyOXubYduSTCPYAHaK8", type: "Cold" },
                { name: "Orange Juice", price: 4.99, description: "Freshly squeezed orange juice", image: "https://images.unsplash.com/photo-1600271886742-f049cd451bba?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Mineral Water", price: 1.99, description: "Pure bottled water", image: "https://images.unsplash.com/photo-1548839140-29a749e1cf4d?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Rose Drink", price: 3.99, description: "Rose flavored sweet drink", image: "rose drink.g4mq9NJaxhV8AOHXUrV7HgHaE8", type: "Cold" },
                { name: "Ginger Soda", price: 2.99, description: "Sparkling ginger beverage", image: "https://images.unsplash.com/photo-1598614187854-26a60e982dc4?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Lemonade", price: 3.49, description: "Homemade fresh lemonade", image: "https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=400&h=300&fit=crop", type: "Cold" },
                { name: "Coffee", price: 3.99, description: "Freshly brewed coffee", image: "https://images.unsplash.com/photo-1509042239860-f550ce710b93?w=400&h=300&fit=crop", type: "Hot" },
                { name: "Green Tea", price: 3.49, description: "Healthy green tea", image: "https://images.unsplash.com/photo-1564890369478-c89ca6d9cde9?w=400&h=300&fit=crop", type: "Hot" }
            ]
        };

        let cart = {};
        let isOpen = false;

        const chatButton = document.getElementById('chatButton');
        const chatContainer = document.getElementById('chatContainer');
        const closeBtn = document.getElementById('closeBtn');
        const chatMessages = document.getElementById('chatMessages');
        const chatInput = document.getElementById('chatInput');
        const sendBtn = document.getElementById('sendBtn');
        const categoryButtons = document.getElementById('categoryButtons');
        const cartCount = document.getElementById('cartCount');
        const viewCartBtn = document.getElementById('viewCartBtn');

        chatButton.addEventListener('click', () => {
            chatContainer.classList.add('active');
            chatButton.style.display = 'none';
            if (!isOpen) {
                setTimeout(() => {
                    addBotMessage("Welcome to Spice Garden! 🍽️ I'm here to help you explore our delicious menu. What would you like to try today?");
                    categoryButtons.classList.add('show');
                }, 500);
                isOpen = true;
            }
        });

        closeBtn.addEventListener('click', () => {
            chatContainer.classList.remove('active');
            chatButton.style.display = 'flex';
        });

        sendBtn.addEventListener('click', sendMessage);
        chatInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') sendMessage();
        });

        viewCartBtn.addEventListener('click', showCart);

        document.querySelectorAll('.category-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                const category = e.target.dataset.category;
                showCategory(category);
            });
        });

        function sendMessage() {
            const message = chatInput.value.trim();
            if (message) {
                addUserMessage(message);
                chatInput.value = '';
                setTimeout(() => {
                    addBotMessage("Thank you! Please browse our menu categories above or check your cart. 🛒");
                }, 800);
            }
        }

        function addBotMessage(text) {
            const messageDiv = document.createElement('div');
            messageDiv.className = 'message bot';
            messageDiv.innerHTML = `<div class="message-content">${text}</div>`;
            chatMessages.appendChild(messageDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function addUserMessage(text) {
            const messageDiv = document.createElement('div');
            messageDiv.className = 'message user';
            messageDiv.innerHTML = `<div class="message-content">${text}</div>`;
            chatMessages.appendChild(messageDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function showCategory(category) {
            const categoryNames = {
                veg: 'Vegetarian Dishes',
                nonveg: 'Non-Vegetarian Delights',
                beverages: 'Refreshing Beverages'
            };

            addUserMessage(`Show me ${categoryNames[category]}`);
            
            setTimeout(() => {
                addBotMessage(`Here are our ${categoryNames[category]}! Click "Add to Cart" to order. 🍴`);
                displayMenuItems(category);
            }, 500);
        }

        function displayMenuItems(category) {
            const items = menuData[category];
            const menuGrid = document.createElement('div');
            menuGrid.className = 'menu-grid';

            items.forEach(item => {
                const card = document.createElement('div');
                card.className = 'menu-card';
                
                const badge = item.spice 
                    ? `<span class="menu-card-badge spice-badge">🌶️ ${item.spice}</span>`
                    : `<span class="menu-card-badge type-badge">${item.type === 'Hot' ? '☕' : '🧊'} ${item.type}</span>`;

                card.innerHTML = `
                    <div class="menu-card-image-container">
                        <img src="${item.image}" alt="${item.name}" class="menu-card-image">
                        <div class="menu-card-price">$${item.price.toFixed(2)}</div>
                    </div>
                    <div class="menu-card-body">
                        <h3 class="menu-card-title">${item.name}</h3>
                        <p class="menu-card-description">${item.description}</p>
                        <div class="menu-card-footer">
                            ${badge}
                            <button class="order-btn" data-name="${item.name}" data-price="${item.price}">Add to Cart</button>
                        </div>
                    </div>
                `;
                
                const orderBtn = card.querySelector('.order-btn');
                orderBtn.addEventListener('click', () => {
                    addToCart(item.name, item.price);
                });
                
                menuGrid.appendChild(card);
            });

            chatMessages.appendChild(menuGrid);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function addToCart(itemName, itemPrice) {
            if (cart[itemName]) {
                cart[itemName].quantity++;
            } else {
                cart[itemName] = {
                    price: itemPrice,
                    quantity: 1
                };
            }
            
            updateCartCount();
            addUserMessage(`Added ${itemName} to cart`);
            
            setTimeout(() => {
                addBotMessage(`Great choice! ${itemName} has been added to your cart. 🎉 Click the Cart button to view your order!`);
            }, 500);
        }

        function updateCartCount() {
            let totalItems = 0;
            for (let item in cart) {
                totalItems += cart[item].quantity;
            }
            cartCount.textContent = totalItems;
        }

        function removeFromCart(itemName) {
            delete cart[itemName];
            updateCartCount();
            chatMessages.innerHTML = '';
            showCart();
        }

        function showCart() {
            addUserMessage('Show my cart');
            
            setTimeout(() => {
                let totalItems = 0;
                let totalPrice = 0;
                
                for (let item in cart) {
                    totalItems += cart[item].quantity;
                    totalPrice += cart[item].price * cart[item].quantity;
                }
                
                if (totalItems === 0) {
                    addBotMessage('Your cart is empty! Browse our menu and add some delicious items. 🍽️');
                    return;
                }
                
                addBotMessage('Here\'s your cart summary:');
                
                const cartDiv = document.createElement('div');
                cartDiv.className = 'cart-summary';
                
                let cartHTML = '<h3>🛒 Your Order</h3>';
                
                for (let item in cart) {
                    const itemTotal = cart[item].price * cart[item].quantity;
                    cartHTML += `
                        <div class="cart-item">
                            <div class="cart-item-info">
                                <span class="cart-item-name">${item}</span>
                                <span class="cart-item-qty">x${cart[item].quantity}</span>
                            </div>
                            <span class="cart-item-price">$${itemTotal.toFixed(2)}</span>
                            <button class="cart-item-remove" data-item="${item}">Remove</button>
                        </div>
                    `;
                }
                
                cartHTML += `
                    <div class="cart-total">
                        <span class="cart-total-label">Total Amount:</span>
                        <span class="cart-total-amount">$${totalPrice.toFixed(2)}</span>
                    </div>
                    <button class="checkout-btn" id="checkoutBtn">Proceed to Checkout 💳</button>
                `;
                
                cartDiv.innerHTML = cartHTML;
                chatMessages.appendChild(cartDiv);
                
                cartDiv.querySelectorAll('.cart-item-remove').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        removeFromCart(e.target.dataset.item);
                    });
                });
                
                cartDiv.querySelector('#checkoutBtn').addEventListener('click', checkout);
                
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }, 500);
        }

        function checkout() {
            let totalPrice = 0;
            let itemsList = '';
            
            for (let item in cart) {
                totalPrice += cart[item].price * cart[item].quantity;
                itemsList += `${item} (x${cart[item].quantity}), `;
            }
            
            itemsList = itemsList.slice(0, -2);
            
            addUserMessage('Proceed to checkout');
            
            setTimeout(() => {
                addBotMessage(`Thank you for your order! 🎉\n\nOrder Summary:\n${itemsList}\n\nTotal: $${totalPrice.toFixed(2)}\n\nYour order will be prepared shortly. Enjoy your meal! 😊`);
                cart = {};
                updateCartCount();
            }, 800);
        }
        
    </script>
    
</body>
</html>
