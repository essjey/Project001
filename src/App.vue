<script setup>
import products from './json/products.json'
import downArrow from './assets/downArrow.vue'
import notification from './assets/bell.vue'
import cart from './assets/cart.vue'
import listView from './assets/list-view.vue'
import square2x2 from './assets/square2x2.vue'
import info from './assets/infoCircle.vue'
// import chevronUpDown from './assets/chevronUpDown.vue'
import plus from './assets/plus.vue'
import fav from './assets/heart.vue'
</script>
<template>
    <header class="nav-wrapper">
        <div class="logo-wrapper">
            <a href="#">Company</a> 
            <span>|</span>
            <button class="lang-selector">
                en <downArrow />
            </button>
        </div>
        <nav class="nav-wrapper">
            <a href="#">Browse</a>
            <a href="#">Search</a>
            <a href="#">Shipping</a>
            <a href="#" class="active">Profile</a>
            <a href="#">Help</a>
            <a href="#">News</a>
        </nav>
        <ul class="user-menu">
            <span>|</span>
            <li class="user-menu--notifications">
                <notification />
            </li>
            <span>|</span>
            <li class="user-menu--cart">
                <cart />
                <span class="badge">1</span>
            </li>
            <span>|</span>
            <li class="user-menu--profile">
                <img src="https://via.placeholder.com/80x80" alt="User Profile Image" class="user-menu--profile-img"> 
                <downArrow />
            </li>
        </ul>     
    </header>
    <div class="promo"><info /> 
        <div class="promo--message">
            <p>{{ promoMessage }}</p> 
        </div>
        <button class="close"><plus /></button>
    </div>
    <main>
        <aside class="sidebar">
            <section class="profile-links">
                <header>
                    <strong>Profile</strong>
                </header>
                <ul>
                    <li class="active"><a href="#">Favorites <span class="badge">8</span></a></li>
                    <li v-for="pLink in profileLinks">
                        <a :href="pLink.link">{{ pLink.name }} <span class="badge">{{ pLink.notifications }}</span></a>
                    </li>
                </ul>
            </section>
            <section class="payment-methods">
                <header>
                    <strong>Payment Method</strong>
                </header>
                <ul class="payment-methods--content">
                    <li v-for="method in paymentMethods" class="payment-methods--item">
                        <div class="payment-methods--item-icon">
                            <img src="https://via.placeholder.com/150x80" alt="Credit Card Icon">
                        </div>
                        <div class="payment-methods--item-text">
                            <p>{{ method.name }}</p>
                            <p>{{ method.number }}</p>
                        </div>
                    </li>
                </ul>
                <footer>
                    <button class="payment-methods--add"><plus /> Add Payment Method</button>
                </footer>
            </section>
        </aside>
        <section class="product-wrapper">
            <nav class="product-nav">
                <div class="product-nav--left">
                    <h4>Favorites <span class="header-note">({{ products.length }})</span></h4>
                </div>
                <div class="product-nav--right">
                    <button class="product-nav--list-view"><listView /></button>
                    <button class="product-nav--grid-view active"><square2x2 /></button>
                    <!-- <div class="sorting-wrapper">                    
                        <select name="sorting" id="sortProducts">
                            <option value="dateDown" selected>Date (Down)</option>
                        </select>
                        <span class="sorting-wrapper--icon"><chevronUpDown /></span>
                    </div> -->
                </div>
            </nav>
            <div class="product-wrapper--inner">
                <div class="productCard" v-for="product in products">
                    <img src="https://via.placeholder.com/650x400" alt="">
                    <div class="productCard--inner">
                        <h3 class="productCard--title">{{ product.name }}</h3>
                        <span class="productCard--tags">Sedan</span>
                        <span class="productCard--tags">Used Car</span>
                        <span class="productCard--tags">SUV</span>
                        <div class="productCard--traveled">
                            <strong class="label">Mileage:</strong>
                            {{ product.traveled }}</div>
                        <div class="productCard--location">
                            <strong class="label">Location:</strong>
                            {{ product.location }}
                        </div>
                        <!-- <div class="productCard--desc">{{ product.description }}</div> -->
                        <div class="productCard--price">
                            <strong class="label">Buy:</strong>
                            {{ product.price }}</div>
                        <button class="productCard--fav"><fav /> Favorite</button>
                    </div>
                </div>
            </div>
            <button class="product-wrapper--more">Show More</button>
        </section>
    </main>
</template>
<script>
/**
 * Reference for Design: 
 * https://dribbble.com/shots/20728751-Favorites-Cars-Automotive-Website
 */
export default {
    data() {
        return {
            promoMessage: 'Example Promo Messaging!',
            profileLinks: [
                {
                    name: "Favorites",
                    notifications: "6",
                    link: "#"
                },
                {
                    name: "Bids",
                    notifications: "2",
                    link: "#"
                }
            ],
            paymentMethods: [
                {
                    name: "Visa",
                    number: "****-1234"
                },
                {
                    name: "Mastercard",
                    number: "****-4321"
                }
            ]
        }
    }
}
</script>

<style scoped>
main {
    padding: 0;
}
main, .promo {
    max-width: 1200px;
    margin-left: auto;
    margin-right: auto;
}
header.nav-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 1rem;
    background: linear-gradient(#47484c, #302f32);
}
.nav-wrapper nav {
    display: flex;
    flex-direction: column;
    text-align: center;
}
.logo-wrapper {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
}
.logo-wrapper span {
    margin-left: 10px;
    margin-right: 10px;
    display: inline-block;
    color: #595959;
}
.logo-wrapper button {
    display: flex;
    text-transform: uppercase;
    font-size: 12px;
    line-height: 1.25rem;
    background-color: transparent;
}
.nav-wrapper nav a, 
.logo-wrapper a {
    color: #848687;
    text-decoration: none;
}
.nav-wrapper nav a.active,
.logo-wrapper a {
    color: #fff;
}
.logo-wrapper a {
    font-weight: bold;
}
.user-menu {
    display: flex;
    align-items: center;
    width: 100%;

}
.user-menu > span {
    display: none;
}
.user-menu li {
    list-style: none;
    margin-left: 1rem;
}
.user-menu--cart .badge {
    background-color: #f57f32;
    padding: .05rem .35rem;
    border-radius: 1rem;
    font-size: 12px;
    position: relative;
    top: -1rem;
    right: .25rem;
}
.user-menu--profile {
    flex-grow: 2;
    text-align: right;
    display: flex;
    align-items: center;
}
.user-menu--profile-img {
    max-width: 50px;
    border-radius: 25px;
}
@media screen and (min-width: 768px) {
    .logo-wrapper {
        margin-bottom: 0px;
    }
    header.nav-wrapper {
        flex-direction: row;
        flex-wrap: nowrap;
        justify-content: space-between;
        padding-left: 1rem;
        padding-right: 1rem;
        padding-top: 0;
        position: relative;
    }
    .nav-wrapper nav {
        margin-top: -1rem;
        margin-bottom: -1rem;
        flex-direction: row;
        justify-content: center;
        align-items: center;
    }
    .nav-wrapper nav a {
        display: inline-block;
        margin-left: 1rem;
        margin-right: 1rem;
        padding-top: 1.05rem;
        padding-bottom: 1.05rem;
        border-bottom: 3px solid transparent;
    }
    .nav-wrapper nav a:hover {
        color: #fff;
        background-color: transparent;
        border-color: #fff;
    }
    .user-menu {
        margin-top: .25rem;
        margin-bottom: .25rem;
        width: auto;
    }
    .user-menu--profile {
        flex-grow: 0;
    }
    .user-menu > span {
        display: inline-block;
        margin-left: 1rem;
        color: #595959;
    }
}

.promo {
    padding: 0rem .25rem;
    margin: 1rem;
    font-family: sans-serif;
    font-weight: bold;
    border-radius: 4px;
    background-color: #249af2;
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
.promo svg {
    margin-left: .5rem;
    margin-right: .5rem;
}
.promo .close  {
    background-color: transparent;
}
.promo--message {
    flex-grow: 2;
}
.promo .close svg {
    transform: rotate(45deg);
}
@media screen and (min-width: 768px) {
    .promo {
        margin: 3rem auto;
    }
}
.sidebar > section, .product-wrapper {
    background-color: #2b2d2e;
    border-radius: 4px;
    margin-bottom: 1.5rem;
}
.product-nav {
    display: flex;
    justify-content: space-between;
    padding-left: 1rem;
    padding-right: 1rem;
}
[class*="product-nav--"].active {
    color: #249af2;
}
.product-wrapper--inner {
    margin-bottom: 2rem;
    padding-right: 1rem;
    padding-left: 1rem;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 1rem;
}
@media screen and (min-width: 768px) {
    .product-wrapper--inner {
        grid-template-columns: 1fr 1fr;
    }
}
@media screen and (min-width: 960px) {
    .product-wrapper--inner {
        grid-template-columns: 1fr 1fr 1fr;
    }
}
/* @media screen and (min-width: 1100px) {
    .product-wrapper--inner {
        grid-template-columns: 1fr 1fr 1fr 1fr;
    }
} */
.product-wrapper--more {
    display: block;
    background-color: #37393b;
    text-align: center;
    width: calc(100% - 2rem);
    margin-left: 1rem;
    margin-right: 1rem;
    padding: .5rem;
    margin-bottom: 1rem
}
.product-nav--right {
    display: flex;
    align-items: center;
}
.header-note {
    font-weight: 100;
}
.sorting-wrapper select {
    appearance: none;
    text-overflow: '';
}
.productCard {
    text-align: left;
    background-color: #454749;
    box-shadow: 0 5px 15px #111111;
}
.productCard--tags {
    display: inline-block;
    color: #fff;
    background-color: #696b6c;
    border-radius: 7px;
    margin-right: 5px;
    padding: 1px 7px;
}
.productCard--inner {
    padding: 0 1rem 1rem;
}
.productCard--inner .label {
    font-size: .75rem;
    color: #a1a3a4;
    display: block;
    margin-top: 5px;
}
.productCard--fav {
    background-color: transparent;
    display: flex;
    width: 100%;
    justify-content: center;
    align-items: center;
    border: 1px solid #848687;
    border-radius: 4px;
    padding: .25rem;
    margin-top: 1rem;
}
.productCard--fav:hover {
    background-color: #ef3a39;
    border-color: transparent;
}
.productCard--fav svg {
    margin-right: 5px;
}
main {
    display: flex;
    flex-direction: column;
}
@media screen and (min-width: 768px) {
    main {
        flex-direction: row;
        flex-direction: nowrap;
    }
    .sidebar {
        width: 35%;
        padding-right: 1rem;
    }
    .product-wrapper {
        flex-grow: 2;
    }
}
aside .badge {
    background-color: #4a4c4e;
    padding: 0rem .5rem;
    border-radius: 1rem;
}
.profile-links li.active {
    background-color: #333536;
}
aside ul {
    padding-left: 0px;
}
.profile-links li a { 
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
    color: #fff;
    text-decoration: none;
}
main header {
    border-bottom: 1px solid #3d3f40;
    padding: 1rem;
}
main footer {
    border-top: 1px solid #3d3f40;
}
footer button {
    display: flex;
    width: 100%;
    line-height: 1.5rem;
    padding: 1rem;
    color: #249af2;
    border-radius: 0 0 4px 4px;background-color: transparent;
}
footer button svg {
    margin-right: 5px;
}
body button:hover, a:hover {
    background-color: rgba(255,255,255,.05);
}
.payment-methods--content {
    padding: 1rem;
}
.payment-methods--content p {
    margin: 0px;
}
.payment-methods--item {
    margin-bottom: 1rem;
    display: flex;
}
.payment-methods--item-icon {
    max-width: 100px;
    margin-right: 1rem;
}
</style>
