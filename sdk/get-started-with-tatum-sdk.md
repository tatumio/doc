# Get started with Tatum SDK

## Build your first dapp with Tatum SDK 🚀

🎯 Welcome to the Tatum SDK Demo: Simplifying Blockchain Development! 🚀

In this step-by-step guide, we'll showcase just how remarkably easy it is to work with the Tatum SDK and retrieve the balance of an Ethereum address using vanilla JavaScript. 💰 Get ready to witness the power of simplicity!

With the Tatum SDK, fetching the balance is a breeze, thanks to its intuitive API. 🌟 No complex setup or convoluted coding required! Just a few lines of vanilla JavaScript code, and we'll connect to the Tatum SDK, retrieve the balance, and display it on a user-friendly interface. 🌐💡

Join us as we embark on our journey to build a Tatum DApp with vanilla JavaScript. Let's break it down into simple steps:

1. Create a new Node.js project and install the Tatum SDK package. 📦
2. Build an HTML page with an input field and a button. This will allow users to enter the Ethereum address and initiate the balance retrieval process. 💻
3. Write vanilla JavaScript code that leverages the Tatum SDK's address.getBalance() method. This function will fetch the balance of the provided Ethereum address. 🤑
4. Launch our application using the Parcel server. Sit back and watch as our vanilla JavaScript-powered DApp comes to life, fetching and displaying the balance in a decentralized, secure, and efficient manner. 🚀

So, grab your coding hat, and let's get started on our Tatum SDK adventure with the simplicity of vanilla JavaScript! 💪

### 1. Create a new project 🆕

The first step is to create a new project by running `npm init` in the terminal. This will prompt you to enter some basic information about the project, such as the project name and version.

```bash
npm init
```

### 2. Install Tatum SDK 📦

Next, you will need to install the Tatum SDK by running `npm install @tatumio/tatum` it in the terminal. This will install the Tatum SDK package and its dependencies.

```bash
npm install @tatumio/tatum
```

### 3. Create an index.html file 📝

After installing the Tatum SDK, you need to create an `index.html` file in your project directory. This file will contain the HTML code that displays the input field, button and a div element for displaying the balance. The button is set up with an event listener that triggers the function to retrieve the balance when clicked. As you can see in the script tag we are import `app.js` which doesn't exist right now, but we will create this file in the next step!

```html
<html>
<head>
    <meta charset="utf-8"/>
    <title>My First Tatum DApp</title>
    <script type="module" src="./app.js"></script>
</head>
<body>
    <h1>Get Eth balance with Tatum!</h1>
    <input type="text" id="address" placeholder="Enter wallet address" />
    <button id="get-balance">Get Balance</button>
    <div id="balance"></div>
</body>
</html>
```

### 4. Create an app.js file 📝

Next, you will create a `app.js` file in your project directory. This file will contain the code that interacts with the Tatum SDK to retrieve the balance of a given Ethereum wallet address.

```javascript
import { TatumSDK, Network } from '@tatumio/tatum'

const button = document.getElementById('get-balance');
const addressInput = document.getElementById('address');
const balanceDiv = document.getElementById('balance');

button.addEventListener('click', async () => {
    const tatum = await TatumSDK.init({ network: Network.ETHEREUM });
    const balance = await tatum.address.getBalance({
        addresses: [addressInput.value],
    });
    const balanceData = balance.data[0];
    balanceDiv.textContent = `${balanceData.balance} ${balanceData.asset}`;
});

```

You initialise the Tatum SDK by calling and passing in the `Network` object for the Ethereum network. Then you call `tatum.address.getBalance` and pass in an object with an array of addresses to retrieve the balance for. Finally, you display the retrieved balance in the balance div element.

{% hint style="info" %}
There are various blockchain networks available - each instance of the TatumSDK is tied to 1 specific network. All supported networks are available [here](https://github.com/tatumio/tatum-js/blob/master/src/dto/Network.ts).
{% endhint %}

### 5. Update package.json 📝

To start the app from the `index.html` file, you need to update the `source` property in your `package.json` file.

```json
{
  "name": "my-first-tatum-dapp",
  "version": "1.0.0",
  "source": "./index.html",
  "license": "MIT",
  "dependencies": {
    "@tatumio/tatum": "^3.0.0"
  }
}
```

### 6. Start server 🚀

The last step is to start the server using Parcel. You can run `npx parcel` in the terminal to start the server, and your app will be available at `http://localhost:1234`.

```bash
npx parcel
```

{% embed url="https://codepen.io/tatum-devrel/pen/MWzZXqz" %}
Get native ETH balance dapp
{% endembed %}

You can enter a wallet address and click the "Get Balance" button to retrieve the balance for that Ethereum address. The balance will be displayed below the button.

{% hint style="info" %}
👉 Hint: Parcel will automatically bundle and serve your app.&#x20;
{% endhint %}

All the files we created together are available on our [TatumSDK repository on github](https://github.com/tatumio/example-apps) 📁.

#### 🎉  Congratulations! You have successfully built your first DApp using TatumSDK!

\
🎉 With just a few lines of vanilla JavaScript code, you were able to connect to the Ethereum blockchain network and retrieve the balance for a given Ethereum wallet address. Now, it's time to explore the full power of Tatum!

🚀 TatumSDK opens up a world of possibilities for your vanilla JavaScript-powered blockchain development journey. Whether you're building decentralised finance (DeFi) applications, NFT platforms, or integrating blockchain into your existing projects, TatumSDK has got you covered.

👨‍💻 To unlock the full potential of TatumSDK and discover its extensive features, head over to our Tatum Dashboard at [dashboard.tatum.io](https://dashboard.tatum.io). Sign up for an account and gain access to a range of powerful tools and services that will accelerate your blockchain development.

🌟 The Tatum Dashboard provides a user-friendly interface to manage your API keys, create notifications, and much more. It's your gateway to streamline your blockchain development process.

🔔 In addition, if you're interested in learning more about specific topics like NFTs, wallet operations, and RPCs, be sure to check out the comprehensive [Tatum Notifications Documentation](https://docs.tatum.io/docs/notifications) for detailed insights and step-by-step guides. This resource will help you dive deeper into advanced functionalities and unleash the full potential of TatumSDK.

👋 Thank you for following along with this guide and taking your first steps into the exciting world of blockchain development with TatumSDK. Get ready to unleash the true potential of decentralised applications!

👉 Don't forget to check out other example apps on our [TatumSDK repository on GitHub](https://github.com/tatumio/example-apps). Happy coding! 🌟
