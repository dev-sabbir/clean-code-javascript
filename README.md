আসল রিপোজিটরি: ryanmcdermott/clean-code-javascript

# clean-code-javascript

## সূচিপত্র
1. [ভূমিকা](#ভূমিকা)
2. [ভ্যারিয়েবলস](#ভ্যারিয়েবলস)
3. [ফাংশনস](#ফাংশনস)
4. [অবজেক্ট এবং ডাটা স্ট্রাকচার](#অবজেক্ট-এবং-ডাটা-স্ট্রাকচার)
5. [ক্লাস](#ক্লাস)
6. [সলিড(SOLID)](#solid)
7. [টেস্টিং](#টেস্টিং)
8. [কনকারেন্সি](#কনকারেন্সি)
9. [এরর হ্যান্ডলিং](#এরর-হ্যান্ডলিং)
10. [ফরম্যাটিং](#ফরম্যাটিং)
11. [কমেন্টস](#কমেন্টস)
12. [অনুবাদ](#অনুবাদ)

## **ভূমিকা**

![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](https://www.osnews.com/images/comics/wtfm.jpg)

এখানে রবার্ট সি. মার্টিন এর [_Clean Code_ ](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) বইয়ে বর্নিত সফটওয়্যার ইঞ্জিনিয়ারিং এর নীতিগুলোকে জাভাস্ক্রিপ্ট এর জন্য কিছুটা পরিবর্তিত করা হয়েছে। এটা কোন স্টাইল গাইড না। এটা হল জাভাস্ক্রিপ্টের মাধ্যমে [সুপাঠ্য, পুনব্যবহারযোগ্য, রিফ্যাক্টরযোগ্য](https://github.com/ryanmcdermott/3rs-of-software-architecture) সফটওয়্যার তৈরি করার গাইড। 

ব্যাপারটা এমন না যে এখানে বর্নিত সব নিয়ম কঠোরভাবে মেনে চলতে হবে, এমনকি এখানে বর্নিত খুব কম নিয়মের সাথে সবাই একমত। এগুলো নির্দেশিকা ব্যাতিত কিছুই না। তবে এগুলো _Clean Code_ বইয়ের লেখকদের বহু বছরের সমষ্টিগত অভিজ্ঞতা থেকে বিধিবদ্ধ করা। 

আমাদের সফটওয়ার ইঞ্জিনিয়ারিং শিল্পের বয়স ৫০ বছরের কিছু বেশি এবং আমরা এখনও অনেক কিছু শিখছি। যখন সফটওয়ার আর্কিটেকচার স্থাপত্যকলার মত পুরনো হবে, তখন হয়ত আমরা মেনে চলার জন্য কিছু কঠোর নিয়ম পাব। সেদিনের আগ পর্যন্ত আমরা যে জাভাস্ক্রিপ্ট কোড তৈরি করছি তার মান যাচাই করার জন্য এই নির্দেশিকাটিকে ব্যবহার করতে পারি। 

ভূমিকা শেষ করার আগে একটা কথা, এই নিয়ম গুলো জানলেই তুমি আগের থেকে ভালো সফটওয়্যার ডেভেলপার  হয়ে যাবে না এবং এগুলো অনেক বছর ধরে মেনে চলা মানে এই না যে তুমি আর ভুল করবে না। মাটির দলা থেকে যেমন বিভিন্ন আকৃতি তৈরি হয়, তেমনি প্রতিটা কোড শুরু হয় প্রথম খসড়া থেকে। আমরা যখন সবশেষে আমাদের সহকর্মীদের সাথে কোড রিভিও করতে বসি তখন আমাদের কোডের অসম্পূর্ণতাগুলোকে চেঁছে ফেলে দিই। প্রথম খসড়াতে ভুল থাকবেই। এজন্য নিজেকে শাস্তি দিও না, বরং তোমার কোড ঝেড়েমুছে ঠিক কর। 

## **ভ্যারিয়েবলস**

### ভ্যারিয়েবল এর নাম অর্থবহ হতে হবে

**খারাপ কোড:**

```javascript
const yyyymmdstr = moment().format("YYYY/MM/DD");
```

**ভালো কোড:**

```javascript
const currentDate = moment().format("YYYY/MM/DD");
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### একই ধরণের ভ্যারিয়েবলের নামকরনের জন্য একই ধরণের শব্দ ব্যবহার করতে হবে। 

**খারাপ কোড:**

```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```

**ভালো কোড:**

```javascript
getUser();
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### খুঁজতে সুবিধা হয় এমন নাম ব্যবহার করতে হবে

আমরা আমাদের ডেভেলপার জীবনে যত কোড লিখব, পড়তে হবে তার থেকে অনেক বেশি। একারণে সুপাঠ্য এবং সহজে খুঁজে পাওয়া যায় এমন কোড লিখা খুবই গুরুত্তপুর্ন। আমরা যদি আমাদের লিখা প্রোগ্রাম বুঝার জন্য ভ্যারিয়েবলের নাম যথেষ্ট অর্থবহ না করি, আমাদের পাঠকদের কষ্ট বাড়বে বই কমবে না। যেসকল ধ্রুবক এবং ভ্যারিয়েবলের নামকরন করা হয় নি সেগুলো চিহ্নিত করতে [buddy.js](https://github.com/danielstjules/buddy.js) এবং [ESLint](https://github.com/eslint/eslint/blob/660e0918933e6e7fede26bc675a0763a6b357c94/docs/rules/no-magic-numbers.md) এর মত টুলগুলো আমাদের  সাহায্য করতে পারে। 

**খারাপ কোড:**

```javascript
// What the heck is 86400000 for?
setTimeout(blastOff, 86400000);
```

**ভালো কোড:**

```javascript
// Declare them as capitalized named constants.
const MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000; //86400000;

setTimeout(blastOff, MILLISECONDS_PER_DAY);
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### নাম দেখেই যেন বুঝা যায় এইরকমভাবে ভ্যারিয়েবল এর নামকরন করতে হবে। 

**খারাপ কোড:**

```javascript
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
saveCityZipCode(
  address.match(cityZipCodeRegex)[1],
  address.match(cityZipCodeRegex)[2]
);
```

**ভালো কোড:**

```javascript
const address = "One Infinite Loop, Cupertino 95014";
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [_, city, zipCode] = address.match(cityZipCodeRegex) || [];
saveCityZipCode(city, zipCode);
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### মেন্টাল ম্যাপিং এড়িয়ে চলতে হবে

নাই মামার চেয়ে কানা মামা ভালো। ভ্যারিয়েবলের নামকরনের সময় এর খেয়াল রাখতে হবে নাম থেকে যেন এর কাজ বুঝা যায়। 

**খারাপ কোড:**

```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(l => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  // Wait, what is `l` for again?
  dispatch(l);
});
```

**ভালো কোড:**

```javascript
const locations = ["Austin", "New York", "San Francisco"];
locations.forEach(location => {
  doStuff();
  doSomeOtherStuff();
  // ...
  // ...
  // ...
  dispatch(location);
});
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### অপ্রয়োজনীয় কন্টেক্সট যোগ করার দরকার নেই

ক্লাস/অবজেক্ট এর নাম থেকে কোন তথ্য জানা গেলে সেই তথ্য আবার ভ্যারিয়েবলের নামের মধ্যে রাখার দরকার নেই। 

**খারাপ কোড:**

```javascript
const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue"
};

function paintCar(car, color) {
  car.carColor = color;
}
```

**ভালো কোড:**

```javascript
const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue"
};

function paintCar(car, color) {
  car.color = color;
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### শর্ট সার্কিটিং/কন্ডিশনাল স্টেটমেন্ট থেকে ডিফন্ট ভ্যালু ব্যবহার করা ভালো। 

শর্ট সার্কিটিং থেকে ডিফল্ট আর্গুমেন্ট  অনেক বেশি পরিচ্ছন্ন। তবে এটা মাথায় রাখতে হবে যে, যদি আমরা ফাংশনে ডিফল্ট আর্গুমেন্ট  ব্যবহার করি তবে অসঙ্গায়িত আর্গুমেন্ট এর ক্ষেত্রেই শুধু মাত্র ডিফল্ট ভ্যালু ব্যবহৃত হবে। অন্যান্য falsy ভ্যালু, যেমনঃ `''`, `""`, `false`, `null`, `0`, এবং `NaN`, এগুলোর পরিবর্তে ডিফল্ট ভ্যালু বসবে না। 

**খারাপ কোড:**

```javascript
function createMicrobrewery(name) {
  const breweryName = name || "Hipster Brew Co.";
  // ...
}
```

**ভালো কোড:**

```javascript
function createMicrobrewery(name = "Hipster Brew Co.") {
  // ...
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **ফাংশনস**

### ফাংশন আর্গুমেন্টস (২টার বেশি নয়, ১ টা হলে ভাল হয়) 

ফাংশন টেস্টিং সহজ করার জন্য, ফাংশন প্যারামিটার কে সীমাবদ্ধ করা খুবই গুরুত্তপুর্ন । ফাংশন প্যারামিটার ৩ এর অধিক হলে, বিন্যাস সমাবেশের কারণে আমাদের টেস্ট কেসের সংখ্যা বেড়ে যায়। 

একদমই অপারগ হলে ৩ টি ফাংশন প্যারামিটার ব্যবহার করা উচিত। তবে আদর্শ হল ২ বা তার কম। এর থেকে বেশি প্যারামিটার হলে তাদেরকে একটা অবজেক্ট এর মধ্যে একত্রীকরণের মাধ্যমে প্যারামিটার এর সংখ্যা কমিয়ে আনতে হবে। 

যেহেতু জাভাস্ক্রিপ্ট এ  অবজেক্ট তৈরি করতে গেলে ক্লাস বয়লারপ্লেট লাগে না, তাই যদি তোমার অনেকগুলো প্যারামিটার প্রয়োজন হয় তবে তুমি অবজেক্ট ব্যবহার করতে পার। 

একটা ফাংশনে কি কি প্যারামিটার আসলে যাচ্ছে তা বুঝানোর জন্য ES2015/ES6 এর destructuring syntax ব্যবহার করতে পার। এটার কিছু সুবিধা আছে, 
1. যখন কেউ ফাংশন সিগনেচার দেখবে তখনি বুঝে ফেলবে কি কি প্যারামিটার দেয়া হচ্ছে ফাংশনের মধ্যে। 
2. Destructring করলে, ফাংশনের আর্গুমেন্ট হিসেবে যে প্রিমিটিভ ভ্যালু দেয়া হয়েছে সেগুলো ক্লোন হয়ে যায়। যা কিনা আমাদের কে সাইড ইফেক্ট প্রতিরোধ করতে সহায়তা করে। তবে মাথায় রাখতে হবে, যদি এরে বা অবজেক্ট destructure করা হয়, সেক্ষেত্রে এরা ক্লোন হয় না। 
3. অব্যবহৃত প্যারামিটার খুঁজে বের করতে লীনটার আমাদের হেল্প করতে পারে। কিন্তু Destructure না করলে হয়ত এটা সম্ভব হত না। 

**খারাপ কোড:**

```javascript
function createMenu(title, body, buttonText, cancellable) {
  // ...
}

createMenu("Foo", "Bar", "Baz", true);

```

**ভালো কোড:**

```javascript
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: "Foo",
  body: "Bar",
  buttonText: "Baz",
  cancellable: true
});
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### প্রতিটা ফাংশনের শুধু মাত্র একটি কাজ করা উচিত

সফটওয়্যার ইঞ্জিনিয়ারিং এ এখন পর্যন্ত এটাই সব থেকে গুরুত্তপুর্ন নীতি। যেসব ফাংশন যদি একের অধিক কাজ করে, সেসব ফাংশন টেস্ট করা, অন্য যায়গায় পুনব্যবহার করা কঠিন হয়ে যায়। একটি ফাংশন যদি কেবল একটি কাজ করে তবে তোমার কোড সুপাঠ্য এবং সহজে পুনরায় লেখা যাবে। তুমি যদি এই গাইডের আর কিছু না গ্রহণ করে  শুধু এই নিয়মটি গ্রহণ কর, তাহলেই তুমি অন্য ডেভেলপের থেকে অনেক এগিয়ে যাবে। 

**খারাপ কোড:**

```javascript
function emailClients(clients) {
  clients.forEach(client => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

**ভালো কোড:**

```javascript
function emailActiveClients(clients) {
  clients.filter(isActiveClient).forEach(email);
}

function isActiveClient(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### ফাংশনের নামেই বলা থাকতে হবে সেটি কি করে

**খারাপ কোড:**

```javascript
function addToDate(date, month) {
  // ...
}

const date = new Date();

// It's hard to tell from the function name what is added
addToDate(date, 1);
```

**ভালো কোড:**

```javascript
function addMonthToDate(month, date) {
  // ...
}

const date = new Date();
addMonthToDate(1, date);
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### ফাংশনে শুধু একধাপ অ্যাবস্ট্রাকশন থাকতে পারবে 

তোমার ফাংশনে একের অধিক ধাপে অ্যাবস্ট্রাকশন থাকা মানেই তোমার ফাংশন একের অধিক কাজ করছে। একে বিভিন্ন ছোটছোট ভাগে বিভক্ত করলে পুনরায় ব্যবহার করা , টেস্টিং করা সহজ হয়ে যায়। 

**খারাপ কোড:**

```javascript
function parseBetterJSAlternative(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach(token => {
    // lex...
  });

  ast.forEach(node => {
    // parse...
  });
}
```

**ভালো কোড:**

```javascript
function parseBetterJSAlternative(code) {
  const tokens = tokenize(code);
  const syntaxTree = parse(tokens);
  syntaxTree.forEach(node => {
    // parse...
  });
}

function tokenize(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(" ");
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      tokens.push(/* ... */);
    });
  });

  return tokens;
}

function parse(tokens) {
  const syntaxTree = [];
  tokens.forEach(token => {
    syntaxTree.push(/* ... */);
  });

  return syntaxTree;
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### ডুপ্লিকেট কোড থাকা যাবে না

তোমার সর্বোচ্চ চেষ্টা করবে যেন ডুপ্লিকেট কোড না থাকে। ডুপ্লিকেট কোড থাকা মানেই, কখনো কোন একটার লজিক পরিবর্তন করা লাগলে তোমার সবগুলো ডুপ্লিকেট কোডে পরিবর্তন করা লাগবে। 

চিন্তা কর তুমি একটা রেস্টুরেন্ট এ আছো এবং তোমার কাজ হচ্ছে রেস্টুরেন্ট এর স্টোরে কি কি আছে সেগুলোর খবর রাখা। মানে হল রেস্টুরেন্টে কতটুকু টমাটো, পেঁয়াজ, হলুদ, মশলা আছে সেগুলোর হিসাব রাখা। তুমি যদি অনেকগুলো যায়গায় এদের হিসাব রাখ, কোন একটার হিশাব কমলে বা বাড়লে তোমার সব লিস্টে পরিবর্তন করা লাগবে। কিন্তু তুমি যদি একটা লিস্টে এদের হিসাব রাখতে তাহলে একটা লিস্টে পরিবর্তন করলেই হত। 

মাঝে মাঝে এমন হয় যে আমাদের ডুপ্লিকেট কোড লিখতে হয়, কারণ দেখা যায়, ২ টা ফাংশন প্রায় একই কাজ করছে শুধু সামান্য একটু পার্থক্য আছে। এই সামান্য পার্থক্যের জন্য আমাদের ২ টা ফাংশন লেখা লাগে। এক্ষেত্রে একটা সমাধান হল, একটা অ্যাবস্ট্রাকশন তৈরি করা। 

এই অ্যাবস্ট্রাকশনটা ঠিকঠাক ভাবে করতে পারা খুবই গুরুত্বপুর্ন। একারণে তোমার উচিত _ক্লাস_ অধ্যায়ে বর্নিত SOLID প্রিন্সিপাল মেনে চলা। ভুল অ্যাবস্ট্রাকশন ডুপ্লিকেট কোড থেকেও ক্ষতিকর, অতএব সাধু সাবধান! তুমি যদি সঠিক ভাবে অ্যাবস্ট্রাকশন তৈরি করতে পার তবে করে ফেল। তা নাহলে একটা পরিবর্তনের জন্য একাধিক জায়গায় পরিবর্তন করা লাগবে। 

**খারাপ কোড:**

```javascript
function showDeveloperList(developers) {
  developers.forEach(developer => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();
    const data = {
      expectedSalary,
      experience,
      githubLink
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach(manager => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();
    const data = {
      expectedSalary,
      experience,
      portfolio### Function names should say what they do
    };

    render(data);
  });
}
```

**ভালো কোড:**

```javascript
function showEmployeeList(employees) {
  employees.forEach(employee => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();

    const data = {
      expectedSalary,
      experience
    };

    switch (employee.type) {
      case "manager":
        data.portfolio = employee.getMBAProjects();
        break;
      case "developer":
        data.githubLink = employee.getGithubLink();
        break;
    }

    render(data);
  });
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### ডিফল্ট অবজেক্ট সেট করার সময় Object.assign ব্যবহার কর

**খারাপ কোড:**

```javascript
const menuConfig = {
  title: null,
  body: "Bar",
  buttonText: null,
  cancellable: true
};

function createMenu(config) {
  config.title = config.title || "Foo";
  config.body = config.body || "Bar";
  config.buttonText = config.buttonText || "Baz";
  config.cancellable =
    config.cancellable !== undefined ? config.cancellable : true;
}

createMenu(menuConfig);
```

**ভালো কোড:**

```javascript
const menuConfig = {
  title: "Order",
  // User did not include 'body' key
  buttonText: "Send",
  cancellable: true
};

function createMenu(config) {
  let finalConfig = Object.assign(
    {
      title: "Foo",
      body: "Bar",
      buttonText: "Baz",
      cancellable: true
    },
    config
  );
  return finalConfig
  // config now equals: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### ফাংশন প্যারামিটার হিসেবে ফ্ল্যাগ ব্যবহার করবে না 

ফ্ল্যাগ ব্যবহার করলে তোমার কোড রিভিওয়ার বুঝতে পারে যে এই ফাংশনটি একাধিক কাজ করছে। যদি ফ্ল্যাগ এর ভ্যালু এর উপর নির্ভর করে তোমার কোডফ্লো বিভিন্ন দিকে যায়, তবে তাদের কে আলাদা ফাংশনে রূপান্তরিত কর। তারপর তোমার ফ্ল্যাগ এর উপর নির্ভর করে বিভিন্ন ফাংশন কে কল কর। 

**খারাপ কোড:**

```javascript
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```

**ভালো কোড:**

```javascript
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### সাইড ইফেক্ট এড়িয়ে চলতে হবে (পার্ট-১)  

যখন একটা ফাংশন ভ্যালু আদানপ্রদান ছাড়া অন্য কাজ করবে তখনই সাইড ইফেক্ট তৈরি হয়। ফাইলে রাইট করা, গ্লোবাল ভ্যারিয়েবল আপডেট করা এগুলো হল সাইড ইফেক্ট এর উদাহরণ। 

মাঝে মাঝে আমাদের সাইড ইফেক্ট এর প্রয়োজন হয়, যেমনঃ ফাইলে রাইট করা। সেক্ষেত্রে আমরা এই সাইড ইফেক্টটাকে একটা আলাদা সার্ভিস বানিয়ে রাখতে পারি। তারপর যেখানে যেখানে দরকার ওই সার্ভিস টা ব্যবহার করতে পারি। 

আসল কথা হল, সাধারণ ভুলগুলো এড়িয়ে চলতে হবে। যেমনঃ অবজেক্ট এর মধ্যে state শেয়ার করা, mutable ডাটা টাইপ ব্যবহার করা, সাইড ইফেক্ট গুলোকে ম্যানেজ না করতে পারা ইত্যাদি। যদি তুমি সাইড ইফেক্ট গুলোকে ঠিকঠাক ম্যানেজ করতে পার তাহলে তুমি বেশিরভাগ প্রোগ্রামারদের থেকে শান্তিতে থাকবে। 

**খারাপ কোড:**

```javascript
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
let name = "Ryan McDermott";

function splitIntoFirstAndLastName() {
  name = name.split(" ");
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**ভালো কোড:**

```javascript
function splitIntoFirstAndLastName(name) {
  return name.split(" ");
}

const name = "Ryan McDermott";
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### সাইড ইফেক্ট এড়িয়ে চলতে হবে (পার্ট-2)  

জাভাস্ক্রিপ্টে primitive ডাটা pass-by-value এবং এরে/অবজেক্ট pass-by-reference পদ্ধতিতে ফাংশনে যায়। এরে এবং অবজেক্ট এর ক্ষেত্রে, যদি তোমার ফাংশন শপিং কার্ট এরেতে ডাটা পরিবর্তন করে তবে অন্য যত ফাংশন cart এরে ব্যবহার করে সবার cart এরে পরিবর্তন হয়ে যাবে। এটা হয়ত ভাল মনে হচ্ছে, একটা খারাপ কেস চিন্তা করা যাক, 

ধর, একজন ব্যবহারকারী তোমার সাইটের "Purchase" বাটন এ ক্লিক করল, যেটা কিনা "purchase" মেথড কে কল করে এবং cart এরে কে নেটওয়ার্ক কলের মাধ্যমে সার্ভার এ প্রেরণ করে। খারাপ ইন্টারনেট কানেকশন এর কারণে, "purchase" ফাংশনকে বারবার নেটওয়ার্কে কল করতে হবে। এখন যদি দুর্ঘটনাবশত তুমি "Add to cart" বাটনে ক্লিক কর তাহলে নতুন আইটেম addItemToCart ফাংশনের মাধ্যমে cart এরেতে যোগ হয়ে যাবে। এবং নতুন আইটেম সহ তোমার রিকুয়েস্ট সার্ভার এ চলে যাবে। 

এটার খুব ভালো একটা সমাধান হল, addToItemCart সব সময় cart কে ক্লোন করে নতুন এরে বানাবে, তারপর সেই এরেতে পরিবর্তন করে নতুন এরে টা রিটার্ন করবে। এতেকরে আসল cart এরে অপরিবর্তিত থাকবে। 

এই পদ্ধতিতে ২ টা কিন্তু আছে, 
1. এমন হতে পারে যে তোমার ইনপুট অব্জেক্টটাই পরিবর্তন করা দরকার, ক্লোন করে কাজ হচ্ছেনা। তবে এটা খুবই কম দেখা যা। বেশিরভাগ জিনিশই সাইড ইফেক্ট ছাড়াই রিফ্যাক্টর করা যায়। 
2. অনেক বড় একটা অবজেক্ট ক্লোন করা পার্ফরমেন্স এর প্রেক্ষিতে খুবই ব্যয়বহুল। সৌভাগ্যবশত বাস্তবে এমন না, কারণ কিছু [অসাধারণ লাইব্রেরি](https://facebook.github.io/immutable-js/) আছে যাদের কারণে অবজেক্ট ক্লোনিং অনেক দ্রুত এবং কম মেমরি ব্যবহার করে করা যায়। 

**খারাপ কোড:**

```javascript
const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};
```

**ভালো কোড:**

```javascript
const addItemToCart = (cart, item) => {
  return [...cart, { item, date: Date.now() }];
};
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### গ্লোবাল ফাংশলে কিছু লিখবে না 

জাভাস্ক্রিপ্টে গ্লোবাল অবজেক্ট এ কিছু পরিবর্তন করা খুবই খারাপ একটি অভ্যাস। কারণ অনেক লাইব্রেরি গ্লোবাল অবজেক্ট ব্যবহার করে। তোমার পরিবর্তন এর কারণে সেইসব লাইব্রেরির কাজের ব্যঘাত ঘটার সম্ভাবনা থাকে। একটা সম্ভাবনা ধরা যাক, 
কি হবে যদি তুমি জাভাস্ক্রিপ্টের ডিফল্ট এরে মেথড এ "diff" নামক একটি মেথড যোগ কর, যেটা কিনা ২ টা এরের মধ্যে পার্থক্য দেখায়। এই মেথডটা Array.prototype এ রাখলে, অন্য লাইব্রেরি যদি একই "diff" নামক মেথড দিয়ে একটা এরের প্রথম এবং শেষ আইটেম এর পার্থক্য দেখাতে চায় তাহলে কি হবে? এই জন্য ES2015/ES6 এর ক্লাস ব্যবহার করে Array গ্লোবাল কে এক্সটেন্ড করে ব্যবহার করা বেশি ভালো। 

**খারাপ কোড:**

```javascript
Array.prototype.diff = function diff(comparisonArray) {
  const hash = new Set(comparisonArray);
  return this.filter(elem => !hash.has(elem));
};
```

**ভালো কোড:**

```javascript
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter(elem => !hash.has(elem));
  }
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### ইম্পেরাটিভ প্রোগ্রামিং থেকে ফাংশনাল প্রোগ্রামিং এ বেশি গুরুত্ব দাও 

জাভাস্ক্রিপ্ট হাস্কেল এর মত ফাংশনাল প্রোগ্রামিং ল্যাঙ্গুয়েজ না। কিন্তু এইটায় একধরনের ফাংশনাল ফ্লেভার আছে। ফাংশনাল ল্যাঙ্গুয়েজ টেস্ট করা তুলনামূলকভাবে সহজ। যখনই পারবে এই স্টাইলে প্রোগ্রামিং করবে, 

**খারাপ কোড:**

```javascript
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500
  },
  {
    name: "Jimmy Gosling",
    linesOfCode: 150
  },
  {
    name: "Gracie Hopper",
    linesOfCode: 1000
  }
];

let totalOutput = 0;

for (let i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

**ভালো কোড:**

```javascript
const programmerOutput = [
  {
    name: "Uncle Bobby",
    linesOfCode: 500
  },
  {
    name: "Suzie Q",
    linesOfCode: 1500
  },
  {
    name: "Jimmy Gosling",
    linesOfCode: 150
  },
  {
    name: "Gracie Hopper",
    linesOfCode: 1000
  }
];

const totalOutput = programmerOutput.reduce(
  (totalLines, output) => totalLines + output.linesOfCode,
  0
);
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### কন্ডিশনাল কে ব্রাকেট দিয়ে আবদ্ধ কর

**খারাপ কোড:**

```javascript
if (fsm.state === "fetching" && isEmpty(listNode)) {
  // ...
}
```

**ভালো কোড:**

```javascript
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === "fetching" && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### নেগেটিভ কন্ডিশনাল এড়িয়ে চল

**খারাপ কোড:**

```javascript
function isDOMNodeNotPresent(node) {
  // ...
}

if (!isDOMNodeNotPresent(node)) {
  // ...
}
```

**ভালো কোড:**

```javascript
function isDOMNodePresent(node) {
  // ...
}

if (isDOMNodePresent(node)) {
  // ...
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### কন্ডিশনাল এড়িয়ে চল

শুরুতে এটা অসম্ভব মনে হতে পারে। বেশিরভাগ মানুষ এটা শুনেই বলবে, "If স্টেটমেন্ট ছাড়া আমি কিভাবে কিছু করবো?" এটার উত্তর হল, আমরা "Polymorphism" ব্যবহার করে এটা করতে পারি। তখন তারা জিজ্ঞেস করবে, "এটা আমি কেন করব?" এটার উত্তর হল, আমরা এতক্ষণ যে ক্লিন কোড এর নিয়মনীতি পরে আসলাম তার মধ্যে একটা, "একটা ফাংশন শুধু একটা কাজ করবে"। যখনই তোমার ফাংশনে if থাকবে তার মানেই হল তোমার ফাংশন একাধিক কাজ করছে। 

**খারাপ কোড:**

```javascript
class Airplane {
  // ...
  getCruisingAltitude() {
    switch (this.type) {
      case "777":
        return this.getMaxAltitude() - this.getPassengerCount();
      case "Air Force One":
        return this.getMaxAltitude();
      case "Cessna":
        return this.getMaxAltitude() - this.getFuelExpenditure();
    }
  }
}
```

**ভালো কোড:**

```javascript
class Airplane {
  // ...
}

class Boeing777 extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude();
  }
}

class Cessna extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getFuelExpenditure();
  }
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### টাইপ চেকিং এড়িয়ে চলতে হবে (পার্ট-১) 

জাভাস্ক্রিপ্টে ফাংশন যেকোন টাইপের ডাটা আর্গুমেন্ট হিসেবে নিতে পারে। মাঝে মধ্যে এই স্বাধীনতাই আমাদের কাল হয়ে দাড়ায়। ফাংশনের ভিতরে টাইপ চেক করা একটা লোভনীয় কাজ। এটা এড়ানর অনেক উপায় আছে। প্রথম কথা হল একটা স্থিতিশীল API ব্যবহার করা। 

**খারাপ কোড:**

```javascript
function travelToTexas(vehicle) {
  if (vehicle instanceof Bicycle) {
    vehicle.pedal(this.currentLocation, new Location("texas"));
  } else if (vehicle instanceof Car) {
    vehicle.drive(this.currentLocation, new Location("texas"));
  }
}
```

**ভালো কোড:**

```javascript
function travelToTexas(vehicle) {
  vehicle.move(this.currentLocation, new Location("texas"));
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### টাইপ চেকিং এড়িয়ে চলতে হবে (পার্ট-2)

তুমি বেসিক প্রিমিটিভ যেমন স্ট্রিং, ইন্টিজারের ক্ষেত্রে polymorphism ব্যবহার করতে পারবে না। কিন্তু তবুও তোমার হয়ত টাইপচেকিং এর দরকার পরতে পারে। তুমি Typescript ব্যবহার করে দেখতে পার। এটা সাধারণ জাভাস্ক্রিপ্টের খুব ভালো একটা বিকল্প। এটা স্ট্যাটিক টাইপিং সাপোর্ট করে।  সাধারণ জাভাস্ক্রিপ্টের প্রব্লেম হল এটায় টাইপচেকিং এর জন্য অনেক কিছু করা লাগে যেটা Typescript এ লাগবে না।  আবারও বলছি Typescript সাধারণ জাভাস্ক্রিপ্টের খুব ভালো একটা বিকল্প। 

**খারাপ কোড:**

```javascript
function combine(val1, val2) {
  if (
    (typeof val1 === "number" && typeof val2 === "number") ||
    (typeof val1 === "string" && typeof val2 === "string")
  ) {
    return val1 + val2;
  }

  throw new Error("Must be of type String or Number");
}
```

**ভালো কোড:**

```javascript
function combine(val1, val2) {
  return val1 + val2;
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### অতিরিক্ত অপ্টিমাইজ করার দরকার নেই 

আধুনিক ব্রাউজার পর্দার পেছনে অনেক ধরণের অপটিমাইজেশন করে। অনেক ক্ষেত্রেই তোমার অপটিমাইজেশন সময়ের অপচয়। কারণ ব্রাউজার এটা নিজেই আবারও করবে। কোথায় অপটিমাইজেশন দরকার সেটা চেক করার জন্য [খুব ভালো রিসোর্স](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers) আছে। আপাতত সগুলো অপ্টিমাইজ করার চেষ্টা কর। 

**খারাপ কোড:**

```javascript
// On old browsers, each iteration with uncached `list.length` would be costly
// because of `list.length` recomputation. In modern browsers, this is optimized.
for (let i = 0, len = list.length; i < len; i++) {
  // ...
}
```

**ভালো কোড:**

```javascript
for (let i = 0; i < list.length; i++) {
  // ...
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### অব্যবহৃত কোড ফেলে দাও 

অব্যবহৃত কোড ডুপ্লিকেট কোড এর মতই খারাপ। তোমার কোডবেজে এগুলোকে রাখার কোন কারণ নেই। তুমি নিশ্চিন্তে অব্যবহৃত কোড ফেলে দিতে পারো। কারণ এগুলো ভার্শন হিস্টরি তে থাকবে। 

**খারাপ কোড:**

```javascript
function oldRequestModule(url) {
  // ...
}

function newRequestModule(url) {
  // ...
}

const req = newRequestModule;
inventoryTracker("apples", req, "www.inventory-awesome.io");
```

**ভালো কোড:**

```javascript
function newRequestModule(url) {
  // ...
}

const req = newRequestModule;
inventoryTracker("apples", req, "www.inventory-awesome.io");
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **অবজেক্ট এবং ডাটা স্ট্রাকচার**

### গেটার সেটার ব্যবহার কর 

অবজেক্ট প্রপার্টি খোজার চেয়ে গেটার সেটার মেথড ব্যবহার করে অবজেক্ট এর ডাটা এক্সেস করা ভালো। তুমি জিজ্ঞেস করতে পারো, কেন? নিচে একটা লিস্ট দিয়ে দিলাম, 

- যখন তুমি অবজেক্ট প্রপার্টি খোজার চেয়ে আরও বেশি কিছু করতে চাও, তখন তোমার সব এক্সেসর পরিবর্তন করা লাগবে না। 
- setter মেথড ব্যবহার করলে ভ্যালিডেশন সহজ হয়। 
- অন্তর্নিহিত অপ্রয়োজনীয় ডাটা আবদ্ধ থাকে 
- getting এবং setting এর সময়  লগ করা, এরর হ্যান্ডলিং করা সহজ হয়। 
- তুমি সার্ভার থেকে ডাটা লোড করার সময় 'lazy-load' করতে পার। 

**খারাপ কোড:**

```javascript
function makeBankAccount() {
  // ...

  return {
    balance: 0
    // ...
  };
}

const account = makeBankAccount();
account.balance = 100;
```

**ভালো কোড:**

```javascript
function makeBankAccount() {
  // this one is private
  let balance = 0;

  // a "getter", made public via the returned object below
  function getBalance() {
    return balance;
  }

  // a "setter", made public via the returned object below
  function setBalance(amount) {
    // ... validate before updating the balance
    balance = amount;
  }

  return {
    // ...
    getBalance,
    setBalance
  };
}

const account = makeBankAccount();
account.setBalance(100);
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### অবজেক্ট এর ভিতরে প্রাইভেট মেম্বার ব্যবহার কর 

এটা তুমি 'closures' ব্যবহার করে করতে পার(ES5 এবং তার নিচে)

**খারাপ কোড:**

```javascript
const Employee = function(name) {
  this.name = name;
};

Employee.prototype.getName = function getName() {
  return this.name;
};

const employee = new Employee("John Doe");
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: undefined
```

**ভালো কোড:**

```javascript
function makeEmployee(name) {
  return {
    getName() {
      return name;
    }
  };
}

const employee = makeEmployee("John Doe");
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
delete employee.name;
console.log(`Employee name: ${employee.getName()}`); // Employee name: John Doe
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **ক্লাস**

### ES2015/ES6 এর ক্লাসকে ES5 এর ফাংশন থেকে বেশি গুরুত্ব দাও 

ES5 এর ক্লাস ব্যবহার করে সুপাঠ্য ক্লাস ইনহেরিটেন্স, কন্সট্রাকশন, মেথড লেখা খুবই কঠিন। তোমার যদি ইনহেরিটেন্স দরকার হয়, সেক্ষেত্রে ES2015/ES6 ক্লাসকে প্রাধান্য দাও। তবে যতক্ষণ না তোমার বড় এবং জটিল অবজেক্ট প্রয়োজন না হচ্ছে ততক্ষণ পর্যন্ত ছোট ফাংশন ব্যবহার কর। 

**খারাপ কোড:**

```javascript
const Animal = function(age) {
  if (!(this instanceof Animal)) {
    throw new Error("Instantiate Animal with `new`");
  }

  this.age = age;
};

Animal.prototype.move = function move() {};

const Mammal = function(age, furColor) {
  if (!(this instanceof Mammal)) {
    throw new Error("Instantiate Mammal with `new`");
  }

  Animal.call(this, age);
  this.furColor = furColor;
};

Mammal.prototype = Object.create(Animal.prototype);
Mammal.prototype.constructor = Mammal;
Mammal.prototype.liveBirth = function liveBirth() {};

const Human = function(age, furColor, languageSpoken) {
  if (!(this instanceof Human)) {
    throw new Error("Instantiate Human with `new`");
  }

  Mammal.call(this, age, furColor);
  this.languageSpoken = languageSpoken;
};

Human.prototype = Object.create(Mammal.prototype);
Human.prototype.constructor = Human;
Human.prototype.speak = function speak() {};
```

**ভালো কোড:**

```javascript
class Animal {
  constructor(age) {
    this.age = age;
  }

  move() {
    /* ... */
  }
}

class Mammal extends Animal {
  constructor(age, furColor) {
    super(age);
    this.furColor = furColor;
  }

  liveBirth() {
    /* ... */
  }
}

class Human extends Mammal {
  constructor(age, furColor, languageSpoken) {
    super(age, furColor);
    this.languageSpoken = languageSpoken;
  }

  speak() {
    /* ... */
  }
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### মেথড চেইনিং ব্যবহার কর 

জাভাস্ক্রিপ্টের এই প্যাটার্নটি খুব উপকারী এবং তুমি অনেক লাইব্রেরি যেমন jQuery, Lodash এ এরকম প্যাটার্ন দেখতে পাবে। এটা তোমার কোড কে অনেক বেশি সহজবোধ্য করে তুলবে। এই জন্য বলি, মেথড চেইনিং ব্যবহার কর এবং দেখ তোমার কোড আগের থেকে অনেক পরিষ্কার হবে। তোমার ক্লাস মেথডের শেষে this রিটার্ন করলেই হবে। তারপর তুমি সেই ফাংশনেও মেথড চেইনিং করতে পারবে। 

**খারাপ কোড:**

```javascript
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
  }

  setModel(model) {
    this.model = model;
  }

  setColor(color) {
    this.color = color;
  }

  save() {
    console.log(this.make, this.model, this.color);
  }
}

const car = new Car("Ford", "F-150", "red");
car.setColor("pink");
car.save();
```

**ভালো কোড:**

```javascript
class Car {
  constructor(make, model, color) {
    this.make = make;
    this.model = model;
    this.color = color;
  }

  setMake(make) {
    this.make = make;
    // NOTE: Returning this for chaining
    return this;
  }

  setModel(model) {
    this.model = model;
    // NOTE: Returning this for chaining
    return this;
  }

  setColor(color) {
    this.color = color;
    // NOTE: Returning this for chaining
    return this;
  }

  save() {
    console.log(this.make, this.model, this.color);
    // NOTE: Returning this for chaining
    return this;
  }
}

const car = new Car("Ford", "F-150", "red").setColor("pink").save();
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### ইনহেরিটেন্স থেকে কম্পোজিশনে গুরুত্ব দাও 

The gang of Four এর লেখা [_ডিজাইন প্যাটার্ন্স_](https://en.wikipedia.org/wiki/Design_Patterns) বইয়ে খুব জনপ্রিয় একটি কথা হল, "যখনই পারবে তখনই ইনহেরিটেন্স থেকে কম্পোজিশন কে বেশি গুরুত্ব দিবে"। ইনহেরিটেন্স ব্যবহারের এবং কম্পোজিশন ব্যবহারের অনেক ভালো কারণ রয়েছে। মোদ্দা কথা হল, তুমি যদি স্বতঃস্ফূর্ত ভাবেই চিন্তা কর যে ইনহেরিটেন্স তোমার সমস্যার সমাধা করবে তবে আরেকবার ভাব যে কম্পোজিশন দিয়ে কাজ টা করা যায় কিনা। অনেক ক্ষেত্রেই তুমি পারবে, 

তুমি হয়ত ভাবতে পার, "তাহলে ইনহেরিটেন্স কখন ব্যবহার করব"? এটা নির্ভর করে তোমার প্রব্লেম এর উপর। যেসব ক্ষেত্রে ইনহেরিটেন্স কম্পজিশন্ থেকে ভালো নিচে তার একটা লিস্ট দিলাম, 

1. তোমার ইনহেরিটেন্স এ "has-a" এর বদলে "is-a" সম্পর্ক বিদ্যমান।  (মানুষ>প্রানি vs. ব্যবহারকারী>ব্যবহারকারির তথ্য ) 
2. তুমি বেজ ক্লাস থেকে কোড পুনরায় ব্যবহার করতে পারলে(human can move like all animals)। 
3. তুমি চাইল্ড ক্লাসে গ্লোবাল পরিবর্তন আনতে চাও বেজ ক্লাসে পরিবর্তনের মাধ্যমে। (Change the caloric expenditure of all animals when they move).

**খারাপ কোড:**

```javascript
class Employee {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  // ...
}

// Bad because Employees "have" tax data. EmployeeTaxData is not a type of Employee
class EmployeeTaxData extends Employee {
  constructor(ssn, salary) {
    super();
    this.ssn = ssn;
    this.salary = salary;
  }

  // ...
}
```

**ভালো কোড:**

```javascript
class EmployeeTaxData {
  constructor(ssn, salary) {
    this.ssn = ssn;
    this.salary = salary;
  }

  // ...
}

class Employee {
  constructor(name, email) {
    this.name = name;
    this.email = email;
  }

  setTaxData(ssn, salary) {
    this.taxData = new EmployeeTaxData(ssn, salary);
  }
  // ...
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **SOLID**

### Single Responsibility Principle (SRP)

ক্লিন কোড বইয়ে যেমনটা বলা হয়েছে, "একটা ক্লাস এ পরিবর্তনের জন্য একটার বেশি কারন থাকা উচিত না"। ফ্লাইটে একটা মাত্র সুটকেস নেয়ার মত, একটা ক্লাসে অনেক ফাংশন ঢুকিয়ে দেয়াটা খুব লোভনীয়।  একটা ক্লাস পরিবর্তন করার হার কমাতে পারাটা গুরুত্বপুর্ন । তুমি যদি ক্লাসে অনেক ফাংশন রাখ, তবে একটা পরিবর্তন কোথায় কিভাবে প্রভাব ফেলছে বুঝতে পারা কঠিন হয়ে যায়। 

**খারাপ কোড:**

```javascript
class UserSettings {
  constructor(user) {
    this.user = user;
  }

  changeSettings(settings) {
    if (this.verifyCredentials()) {
      // ...
    }
  }

  verifyCredentials() {
    // ...
  }
}
```

**ভালো কোড:**

```javascript
class UserAuth {
  constructor(user) {
    this.user = user;
  }

  verifyCredentials() {
    // ...
  }
}

class UserSettings {
  constructor(user) {
    this.user = user;
    this.auth = new UserAuth(user);
  }

  changeSettings(settings) {
    if (this.auth.verifyCredentials()) {
      // ...
    }
  }
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### Open/Closed Principle (OCP)

বারট্রান্ড মেয়ার এর মতে, "সফটওয়ারের ইউনিট(ক্লাস, মডিউলস, ফাংশন্স ইত্যাদি) গুলো এক্সটেন্ড করার জন্য খোলা থাকতে হবে , কিন্তু মডিফিকেশনের জন্য বন্ধ থাকতে হবে" । এটা আসলে কি বুঝায়? এটা দিয়ে আসলে বুঝায়, তোমার ব্যবহারকারীকে নতুন ফাংশন যোগ করতে দিতে হবে, কিন্তু যে ফাংশন আগে থেকে আছে সেগুলো পরিবর্তন করা আটকাতে হবে। 

**খারাপ কোড:**

```javascript
class AjaxAdapter extends Adapter {
  constructor() {
    super();
    this.name = "ajaxAdapter";
  }
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
    this.name = "nodeAdapter";
  }
}

class HttpRequester {
  constructor(adapter) {
    this.adapter = adapter;
  }

  fetch(url) {
    if (this.adapter.name === "ajaxAdapter") {
      return makeAjaxCall(url).then(response => {
        // transform response and return
      });
    } else if (this.adapter.name === "nodeAdapter") {
      return makeHttpCall(url).then(response => {
        // transform response and return
      });
    }
  }
}

function makeAjaxCall(url) {
  // request and return promise
}

function makeHttpCall(url) {
  // request and return promise
}
```

**ভালো কোড:**

```javascript
class AjaxAdapter extends Adapter {
  constructor() {
    super();
    this.name = "ajaxAdapter";
  }

  request(url) {
    // request and return promise
  }
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
    this.name = "nodeAdapter";
  }

  request(url) {
    // request and return promise
  }
}

class HttpRequester {
  constructor(adapter) {
    this.adapter = adapter;
  }

  fetch(url) {
    return this.adapter.request(url).then(response => {
      // transform response and return
    });
  }
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### Liskov Substitution Principle (LSP)

This is a scary term for a very simple concept. It's formally defined as "If S
is a subtype of T, then objects of type T may be replaced with objects of type S
(i.e., objects of type S may substitute objects of type T) without altering any
of the desirable properties of that program (correctness, task performed,
etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class,
then the base class and child class can be used interchangeably without getting
incorrect results. This might still be confusing, so let's take a look at the
classic Square-Rectangle example. Mathematically, a square is a rectangle, but
if you model it using the "is-a" relationship via inheritance, you quickly
get into trouble.

**খারাপ কোড:**

```javascript
class Rectangle {
  constructor() {
    this.width = 0;
    this.height = 0;
  }

  setColor(color) {
    // ...
  }

  render(area) {
    // ...
  }

  setWidth(width) {
    this.width = width;
  }

  setHeight(height) {
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  setWidth(width) {
    this.width = width;
    this.height = width;
  }

  setHeight(height) {
    this.width = height;
    this.height = height;
  }
}

function renderLargeRectangles(rectangles) {
  rectangles.forEach(rectangle => {
    rectangle.setWidth(4);
    rectangle.setHeight(5);
    const area = rectangle.getArea(); // BAD: Returns 25 for Square. Should be 20.
    rectangle.render(area);
  });
}

const rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles(rectangles);
```

**ভালো কোড:**

```javascript
class Shape {
  setColor(color) {
    // ...
  }

  render(area) {
    // ...
  }
}

class Rectangle extends Shape {
  constructor(width, height) {
    super();
    this.width = width;
    this.height = height;
  }

  getArea() {
    return this.width * this.height;
  }
}

class Square extends Shape {
  constructor(length) {
    super();
    this.length = length;
  }

  getArea() {
    return this.length * this.length;
  }
}

function renderLargeShapes(shapes) {
  shapes.forEach(shape => {
    const area = shape.getArea();
    shape.render(area);
  });
}

const shapes = [new Rectangle(4, 5), new Rectangle(4, 5), new Square(5)];
renderLargeShapes(shapes);
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### Interface Segregation Principle (ISP)

জাভাস্ক্রিপ্টে যদিও ইন্টারফেস না থাকার কারণে এই নীতি খাটে না। তবে, এটা গুরুত্বপুর্ন এবং আনুসাংগিক।  ISP অনুযায়ী, " ক্লায়েন্ট যে ইন্টারফেস ব্যবহার করে না সেই ইন্টারফেস চাপিয়ে দেয়া যাবে না। " 
এই নীতিটি বুঝার জন্য একটা ভালো উদাহরণ হল, ক্লাসের সেটিং অবজেক্ট কে আবশ্যিক না করা। এতে করে যে সকল ক্লাসের সেটিং অবজেক্ট অনেক বড় এবং ক্লায়েন্টের সব সেটিং প্রয়োজন নেই, সেখেত্রে আমরা একটা বিশাল ইন্টারফেস বানানো থেকে বেচে যাই। 

**খারাপ কোড:**

```javascript
class DOMTraverser {
  constructor(settings) {
    this.settings = settings;
    this.setup();
  }

  setup() {
    this.rootNode = this.settings.rootNode;
    this.settings.animationModule.setup();
  }

  traverse() {
    // ...
  }
}

const $ = new DOMTraverser({
  rootNode: document.getElementsByTagName("body"),
  animationModule() {} // Most of the time, we won't need to animate when traversing.
  // ...
});
```

**ভালো কোড:**

```javascript
class DOMTraverser {
  constructor(settings) {
    this.settings = settings;
    this.options = settings.options;
    this.setup();
  }

  setup() {
    this.rootNode = this.settings.rootNode;
    this.setupOptions();
  }

  setupOptions() {
    if (this.options.animationModule) {
      // ...
    }
  }

  traverse() {
    // ...
  }
}

const $ = new DOMTraverser({
  rootNode: document.getElementsByTagName("body"),
  options: {
    animationModule() {}
  }
});
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### Dependency Inversion Principle (DIP)

এই মূলনীতি ২টা গুরত্তপুর্ন জিনিস বলে থাকে, 
1. হাই লেভেল মডিউল কখনোই লো লেভেল মডিউল এর উপরে নির্ভর করবে না। 
2. অ্যাবস্ট্রাকশন ডিটেইলের উপর নির্ভর করবেন না। ডিটেইল অ্যাবস্ট্রাকশনের উপরে নির্ভর করবে। 

হয়ত সহজে বুঝবে না, কিন্তু তুমি যদি AngularJS ব্যবহার করে থাক, তাহলে এই মূলনীতির ব্যবহার দেখার কথা। AngularJS ডিপেন্ডেন্সি ইনজেকশনের মধ্যে এই মূলনীতির প্রয়োগ করে। যদিও ২ টা একই ধারণা না। DIP হাই লেভেল মডিউল কে লো লেভেল মডিউল সম্পর্কে জানতে বাধা দেয়। এটার অনেক বড় উপকার হল, এটা মডিউলগুলোর মধ্যে কোন বন্ধন রাখেনা। কাপলিং কোড রেফ্যাক্টরের জন্য খুব খারাপ একটা জিনিস। 

আগেও বলা হয়েছে, জাভাস্ক্রিপ্টে কোন ইন্টারফেস নাই, সুতরাং, এখানে অ্যাবস্ট্রাকশন অন্তর্নিহিত কন্ট্রাক্ট এর উপর নির্ভর করে। মানে একটা ক্লাস/অবজেক্ট অন্য ক্লাস বা অবজেক্ট এর জন্য নিজের যে মেথড বা মেম্বার গুলো উন্মুক্ত করে দেয় তাদেরকে আমরা কন্ট্রাক্ট বলছি। নিচের উদাহরণে, inventoryTracker এর যেকোনো মডিউল এ requestitems মেথড থাকাটাই implicit কন্ট্রাক্ট । 

**খারাপ কোড:**

```javascript
class InventoryRequester {
  constructor() {
    this.REQ_METHODS = ["HTTP"];
  }

  requestItem(item) {
    // ...
  }
}

class InventoryTracker {
  constructor(items) {
    this.items = items;

    // BAD: We have created a dependency on a specific request implementation.
    // We should just have requestItems depend on a request method: `request`
    this.requester = new InventoryRequester();
  }

  requestItems() {
    this.items.forEach(item => {
      this.requester.requestItem(item);
    });
  }
}

const inventoryTracker = new InventoryTracker(["apples", "bananas"]);
inventoryTracker.requestItems();
```

**ভালো কোড:**

```javascript
class InventoryTracker {
  constructor(items, requester) {
    this.items = items;
    this.requester = requester;
  }

  requestItems() {
    this.items.forEach(item => {
      this.requester.requestItem(item);
    });
  }
}

class InventoryRequesterV1 {
  constructor() {
    this.REQ_METHODS = ["HTTP"];
  }

  requestItem(item) {
    // ...
  }
}

class InventoryRequesterV2 {
  constructor() {
    this.REQ_METHODS = ["WS"];
  }

  requestItem(item) {
    // ...
  }
}

// By constructing our dependencies externally and injecting them, we can easily
// substitute our request module for a fancy new one that uses WebSockets.
const inventoryTracker = new InventoryTracker(
  ["apples", "bananas"],
  new InventoryRequesterV2()
);
inventoryTracker.requestItems();
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **টেস্টিং**

প্রোডাক্ট শিপিং এর থেকে টেস্টিং গুরুত্বপুর্ন । যদি তুমি ভালভাবে টেস্ট না কর বা কম টেস্ট কর, তাহলে প্রতিবার শিপিং এর সময় তুমি নিশ্চিত থাকতে পারবে না। পর্যাপ্ত টেস্ট বলতে কি বুঝায় সেটা তোমার টিম এর উপর ডিপেন্ড করে। তবে ১০০% টেস্ট কভারেজ থাকলে তুমি অনেক বেশি আত্মবিশ্বাসী এবং ডেভেলপের হিসেবে শান্তি তে থাকতে পারবে। তার মানে হল ভালো টেস্টিং ফ্রেমওয়ার্ক এর পাশাপাশি [ভালো কভারেজ টুল](https://gotwarlost.github.io/istanbul/) ও প্রয়োজন। 

টেস্ট না লেখার কোন অজুহাত নেই। [অনেক ভালো টেস্ট ফ্রেমওয়ার্ক](https://jstherightway.org/#testing-tools) আছে। সুতরাং, তোমার টিম যেটা পছন্দ করে সেটা বেছে নাও। তারপর প্রতিটা নতুন ফিচার, মডিউল লেখার সময় টেস্ট লেখা নিশ্চিত কর। তুমি যদি Test Driven Development পছন্দ কর তাহলে খুব ভালো। তবে আসল কথা হল, প্রতিটি নতুন ফিচার শিপিং এর আগে টেস্ট কভারেজ নিশ্চিত করা। 

### প্রতি টেস্ট এ একটা মাত্র কনসেপ্ট

**খারাপ কোড:**

```javascript
import assert from "assert";

describe("MomentJS", () => {
  it("handles date boundaries", () => {
    let date;

    date = new MomentJS("1/1/2015");
    date.addDays(30);
    assert.equal("1/31/2015", date);

    date = new MomentJS("2/1/2016");
    date.addDays(28);
    assert.equal("02/29/2016", date);

    date = new MomentJS("2/1/2015");
    date.addDays(28);
    assert.equal("03/01/2015", date);
  });
});
```

**ভালো কোড:**

```javascript
import assert from "assert";

describe("MomentJS", () => {
  it("handles 30-day months", () => {
    const date = new MomentJS("1/1/2015");
    date.addDays(30);
    assert.equal("1/31/2015", date);
  });

  it("handles leap year", () => {
    const date = new MomentJS("2/1/2016");
    date.addDays(28);
    assert.equal("02/29/2016", date);
  });

  it("handles non-leap year", () => {
    const date = new MomentJS("2/1/2015");
    date.addDays(28);
    assert.equal("03/01/2015", date);
  });
});
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **কনকারেন্সি**

### কলব্যাক ব্যবহার না করে, প্রমিস ব্যবহার কর 

কলব্যাক মেথড অনেক বেশি নেস্টিং তৈরি করে। ES2015/ES6 এর সাথে প্রমিস গ্লোবাল টাইপ হিসেবে দেয়া আছে, সেটা ব্যবহার কর। 

**খারাপ কোড:**

```javascript
import { get } from "request";
import { writeFile } from "fs";

get(
  "https://en.wikipedia.org/wiki/Robert_Cecil_Martin",
  (requestErr, response, body) => {
    if (requestErr) {
      console.error(requestErr);
    } else {
      writeFile("article.html", body, writeErr => {
        if (writeErr) {
          console.error(writeErr);
        } else {
          console.log("File written");
        }
      });
    }
  }
);
```

**ভালো কোড:**

```javascript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
  .then(body => {
    return writeFile("article.html", body);
  })
  .then(() => {
    console.log("File written");
  })
  .catch(err => {
    console.error(err);
  });
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### Async/Await প্রমিস থেকেও ভাল 

কলব্যাকের তুলনায় প্রমিস অনেক ভাল। কিন্তু ES2017/ES8 এর সাথে asnyc এবং await আছে, যেটা আরও ভালো সমাধান দিতে পারে। তোমার শুধু ফাংশনের আগে async ব্যবহার করতে হবে। যদি ES2017/ES8 এর সুবিধা নিতে পার তাহলে আজ থেকেই async  এবং await ব্যবহার কর। 

**খারাপ কোড:**

```javascript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

get("https://en.wikipedia.org/wiki/Robert_Cecil_Martin")
  .then(body => {
    return writeFile("article.html", body);
  })
  .then(() => {
    console.log("File written");
  })
  .catch(err => {
    console.error(err);
  });
```

**ভালো কোড:**

```javascript
import { get } from "request-promise";
import { writeFile } from "fs-extra";

async function getCleanCodeArticle() {
  try {
    const body = await get(
      "https://en.wikipedia.org/wiki/Robert_Cecil_Martin"
    );
    await writeFile("article.html", body);
    console.log("File written");
  } catch (err) {
    console.error(err);
  }
}

getCleanCodeArticle()
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **এরর হ্যান্ডলিং**

এরর থ্রু করা একটি ভাল জিনিশ। তার মানে হল তোমার রানটাইম বুঝতে পেরেছে যে কিছু একটা সমস্যা আছে। 

### এরর কে অবজ্ঞা কর না। 

এরর পেলে সেটা নিয়ে কিছু না করলে তুমি এরর এর কারণ বের করতে পারবে না এবং তার সমাধান ও দিতে পারবে না। কনসোলে এরর লগ করা তেমন ভাল কোন সমাধান না। এটা কনসোলে প্রিন্ট হওয়া হাজারও জিনিসের ভিড়ে হারিয়ে যেতে পারে। যদি তুমি তোমার কোড কে try/catch ব্লক এ আবদ্ধ কর তার মানে হল তুমি অনুমান করতে পারছ এখানে একটা এরর হতে পারে। সুতরাং সেক্ষেত্রে তোমার একটা পরিকল্পনা থাকা উচিত। 

**খারাপ কোড:**

```javascript
try {
  functionThatMightThrow();
} catch (error) {
  console.log(error);
}
```

**ভালো কোড:**

```javascript
try {
  functionThatMightThrow();
} catch (error) {
  // One option (more noisy than console.log):
  console.error(error);
  // Another option:
  notifyUserOfError(error);
  // Another option:
  reportErrorToService(error);
  // OR do all three!
}
```

### রিজেক্টেড প্রমিস কে অবজ্ঞা করবে না। 

যেকারনে try/catch এ ধরা এরর কে অবজ্ঞা করবে না। একই কারণে রিজেক্টেড প্রমিসকেও অবজ্ঞা করবে না। 

**খারাপ কোড:**

```javascript
getdata()
  .then(data => {
    functionThatMightThrow(data);
  })
  .catch(error => {
    console.log(error);
  });
```

**ভালো কোড:**

```javascript
getdata()
  .then(data => {
    functionThatMightThrow(data);
  })
  .catch(error => {
    // One option (more noisy than console.log):
    console.error(error);
    // Another option:
    notifyUserOfError(error);
    // Another option:
    reportErrorToService(error);
    // OR do all three!
  });
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **ফরম্যাটিং**

ফরম্যাটিং একটা সাব্জেটিভ ব্যপার। এখানে অন্যে রুলের মতই ফরম্যাটিং এর ও কোন ধরাবাঁধা নিয়ম নেই।  আসল কথা হল, কখনো ফরম্যাটিং নিয়ে তর্ক করবে না। [অনেক টুলস](https://standardjs.com/rules.html)আছে এই কাজ টা অটোম্যাট করার জন্য। যেকোনো একটা ব্যবহার কর। ফরম্যাটিং নিয়ে তর্ক করা সময়ের অপচয় করা ছাড়া আর  কিছু না। 

যেগুলো অটো ফরম্যাটিং এর আওতায় পরে না সেগুলোর জন্য নিচে কিছু নিয়ম দেয়া আছে। 

### স্থিতিশীল ক্যাপিটালাইযেশন ব্যবহার কর। 

যেহেতু জাভাস্ক্রিপ্ট আন্টাইপড ল্যাঙ্গুয়েজ, তাই যথাযথ ক্যাপিটালাইজেশন ভ্যারিয়েবল সম্পর্কে তথ্য দিতে পারে। এই নিয়মগুলোও সাব্জেক্টিভ, তাই তোমাদের টিম এর সুবিধা মত একটা বেছে নিলেই হবে। তবে যেটাই বেছে নাও না কেন সেটাতেই স্থির থেকো। 

**খারাপ কোড:**

```javascript
const DAYS_IN_WEEK = 7;
const daysInMonth = 30;

const songs = ["Back In Black", "Stairway to Heaven", "Hey Jude"];
const Artists = ["ACDC", "Led Zeppelin", "The Beatles"];

function eraseDatabase() {}
function restore_database() {}

class animal {}
class Alpaca {}
```

**ভালো কোড:**

```javascript
const DAYS_IN_WEEK = 7;
const DAYS_IN_MONTH = 30;

const SONGS = ["Back In Black", "Stairway to Heaven", "Hey Jude"];
const ARTISTS = ["ACDC", "Led Zeppelin", "The Beatles"];

function eraseDatabase() {}
function restoreDatabase() {}

class Animal {}
class Alpaca {}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### Function callers and callees should be close

যদি একটা ফাংশন অন্য একটাকে কল করে, তবে চেষ্টা করবে এদেরকে পাশাপাশি রাখতে। 

**খারাপ কোড:**

```javascript
class PerformanceReview {
  constructor(employee) {
    this.employee = employee;
  }

  lookupPeers() {
    return db.lookup(this.employee, "peers");
  }

  lookupManager() {
    return db.lookup(this.employee, "manager");
  }

  getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  perfReview() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();
  }

  getManagerReview() {
    const manager = this.lookupManager();
  }

  getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.perfReview();
```

**ভালো কোড:**

```javascript
class PerformanceReview {
  constructor(employee) {
    this.employee = employee;
  }

  perfReview() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();
  }

  getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  lookupPeers() {
    return db.lookup(this.employee, "peers");
  }

  getManagerReview() {
    const manager = this.lookupManager();
  }

  lookupManager() {
    return db.lookup(this.employee, "manager");
  }

  getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.perfReview();
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **কমেন্টস**

### শুধুমাত্র কমপ্লেক্স বিজনেস লজিক সমৃদ্ধ কোডের ক্ষেত্রে কমেন্ট করবে। 

কমেন্ট হচ্ছে একধরনের ক্ষমা প্রার্থনা। কারণ ভাল _বেশিরভাগ_ ক্ষেত্রেই নিজেই নিজের ডকুমেন্ট হিসবে কাজ করে, কমেন্ট করার দরকার পরে না। 

**খারাপ কোড:**

```javascript
function hashIt(data) {
  // The hash
  let hash = 0;

  // Length of string
  const length = data.length;

  // Loop through every character in data
  for (let i = 0; i < length; i++) {
    // Get character code.
    const char = data.charCodeAt(i);
    // Make the hash
    hash = (hash << 5) - hash + char;
    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

**ভালো কোড:**

```javascript
function hashIt(data) {
  let hash = 0;
  const length = data.length;

  for (let i = 0; i < length; i++) {
    const char = data.charCodeAt(i);
    hash = (hash << 5) - hash + char;

    // Convert to 32-bit integer
    hash &= hash;
  }
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### কখনই কমেন্টেড কোড রাখবেনা

ভার্শন কন্ট্রোল তৈরি হওয়ার একটা কারণ আছে। পুরাতন কোড তোমার হিস্টোরিতেই থাকবে, কমেন্ট করে রাখার দরকার নেই। 

**খারাপ কোড:**

```javascript
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

**ভালো কোড:**

```javascript
doStuff();
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### জার্নাল কমেন্ট লিখবে না। 

মনে রাখবে, ভার্শন কন্ট্রোল ব্যবহার করতে হবে। `git log` ব্যবহার কর হিস্টোরি দেখতে। 

**খারাপ কোড:**

```javascript
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
function combine(a, b) {
  return a + b;
}
```

**ভালো কোড:**

```javascript
function combine(a, b) {
  return a + b;
}
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

### পজিশনাল মার্কার রাখার দরকার নেই। 

এগুলো আসলে শুধু সমস্যা তৈরি করে। 

**খারাপ কোড:**

```javascript
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
$scope.model = {
  menu: "foo",
  nav: "bar"
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
const actions = function() {
  // ...
};
```

**ভালো কোড:**

```javascript
$scope.model = {
  menu: "foo",
  nav: "bar"
};

const actions = function() {
  // ...
};
```

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**

## **অনুবাদ**

This is also available in other languages:

- ![am](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Armenia.png) **Armenian**: [hanumanum/clean-code-javascript/](https://github.com/hanumanum/clean-code-javascript)
- ![bd](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bangladesh.png) **Bangla(বাংলা)**: [InsomniacSabbir/clean-code-javascript/](https://github.com/InsomniacSabbir/clean-code-javascript/)
- ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [fesnt/clean-code-javascript](https://github.com/fesnt/clean-code-javascript)
- ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Simplified Chinese**:
  - [alivebao/clean-code-js](https://github.com/alivebao/clean-code-js)
  - [beginor/clean-code-javascript](https://github.com/beginor/clean-code-javascript)
- ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Traditional Chinese**: [AllJointTW/clean-code-javascript](https://github.com/AllJointTW/clean-code-javascript)
- ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [eugene-augier/clean-code-javascript-fr](https://github.com/eugene-augier/clean-code-javascript-fr)
- ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [marcbruederlin/clean-code-javascript](https://github.com/marcbruederlin/clean-code-javascript)
- ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Indonesia**: [andirkh/clean-code-javascript/](https://github.com/andirkh/clean-code-javascript/)
- ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [frappacchio/clean-code-javascript/](https://github.com/frappacchio/clean-code-javascript/)
- ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/clean-code-javascript/](https://github.com/mitsuruog/clean-code-javascript/)
- ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [qkraudghgh/clean-code-javascript-ko](https://github.com/qkraudghgh/clean-code-javascript-ko)
- ![pl](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Poland.png) **Polish**: [greg-dev/clean-code-javascript-pl](https://github.com/greg-dev/clean-code-javascript-pl)
- ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**:
  - [BoryaMogila/clean-code-javascript-ru/](https://github.com/BoryaMogila/clean-code-javascript-ru/)
  - [maksugr/clean-code-javascript](https://github.com/maksugr/clean-code-javascript)
- ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [tureey/clean-code-javascript](https://github.com/tureey/clean-code-javascript)
- ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Uruguay.png) **Spanish**: [andersontr15/clean-code-javascript](https://github.com/andersontr15/clean-code-javascript-es)
- ![rs](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Serbia.png) **Serbian**: [doskovicmilos/clean-code-javascript/](https://github.com/doskovicmilos/clean-code-javascript)
- ![tr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Turkey.png) **Turkish**: [bsonmez/clean-code-javascript](https://github.com/bsonmez/clean-code-javascript/tree/turkish-translation)
- ![ua](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Ukraine.png) **Ukrainian**: [mindfr1k/clean-code-javascript-ua](https://github.com/mindfr1k/clean-code-javascript-ua)
- ![vi](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [hienvd/clean-code-javascript/](https://github.com/hienvd/clean-code-javascript/)
- ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/clean-code-javascript/](https://github.com/mitsuruog/clean-code-javascript/)
- ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Indonesia**:
  [andirkh/clean-code-javascript/](https://github.com/andirkh/clean-code-javascript/)
- ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**:
  [frappacchio/clean-code-javascript/](https://github.com/frappacchio/clean-code-javascript/)
- ![bd](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bangladesh.png) **Bangla(বাংলা)**:
  [InsomniacSabbir/clean-code-javascript/](https://github.com/InsomniacSabbir/clean-code-javascript/)

**[⬆ উপরে ফিরে যেতে এখানে ক্লিক করতে হবে](#সূচিপত্র)**
