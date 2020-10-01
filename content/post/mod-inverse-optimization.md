---
title: "Modular Inverse Related Optimizations"
date: 2020-10-01T18:04:32+06:00
draft: false
tags: ["Number Theory"]
index: true
description: "Some optimizations related to the modular inverse calculation"
highlight: true
---

##


[মডুলার অ্যারিথমেটিক এবং ইনভার্স সম্পর্কে জানতে এসব লিংকে ঘুরে আসা যেতে পারেঃ [মডুলার অ্যারিথমেটিক](http://www.shafaetsplanet.com/?p=936) , [Modular Inverse](https://cp-algorithms.com/algebra/module-inverse.html)]


কোনো কোনো প্রবলেমে অনেক নাম্বারের মডুলার ইনভার্স প্রিক্যালকুলেট করে রাখতে হয় । তখন TLE থেকে বাঁচতে এই টাইপের অপটিমাইজেশন প্রয়োজন হয় । যেমনঃ [KUET IUPC, 2019](https://algo.codemarshal.org/contests/kuet-iupc-19) এর F নং প্রবলেমটা । সাথে একটা জিনিসও জানা থাকা দরকার । অতিরিক্ত $mod$ অপারেশনও প্রচুর সময় খরচ করে TLE দিতে পারে ।


আলোচনার সুবিধার্থে ধরে নিচ্ছি আমরা মডুলার ইনভার্স বের করব একটি মৌলিক সংখ্যা m এর সাপেক্ষে ।


**প্রবলেম ১ঃ** $n$ দেওয়া আছে । $1!$ থেকে $n!$ পর্যন্ত সবগুলো $i!$ এর মডুলার ইনভার্স বের করতে হবে ।


**সলিউশনঃ** সাধারণ এপ্রোচ হচ্ছে, প্রথমে সবগুলো $1 \leq i \leq n$ এর জন্য $(i! \space mod \space m)$ বের করে রাখা । এরপর প্রত্যেক $1 \leq i \leq n$ এর জন্য $i! \space (mod \space m)$ এর মডুলার ইনভার্স ক্যালকুলেট করা । একটি সংখ্যার মডুলার ইনভার্স বের করার কমপ্লেক্সিটি অভারল $O(logm)$ ধরা হয় । তাহলে প্রত্যেক $1 \leq i \leq n$ এর মডুলার ইনভার্স বের করার কমপ্লেক্সিটি এই মেথডে $O(nlogm)$ ।

  
তবে এটা কিন্তু $O(n)$ এই বের করা সম্ভব ![](https://static.xx.fbcdn.net/images/emoji.php/v9/t2c/1.5/18/1f603.png) । প্রথমে আমরা $n! \space (mod \space m)$ এর মান বের করব একটা লিনিয়ার লুপ চালিয়ে। এরপর শুধু $n! \space (mod \space m)$ এর মডুলার ইনভার্স বের করে রাখব । এখন একটা জিনিস লক্ষ্য করি,

  
![](https://scontent.fdac6-1.fna.fbcdn.net/v/t1.0-9/120453844_353816269151686_4794290400346568219_n.jpg?_nc_cat=108&_nc_sid=32a93c&_nc_ohc=2b2nvGLUDhgAX9mhKzq&_nc_ht=scontent.fdac6-1.fna&oh=94a79716f009c1a093ae53cf46b6899a&oe=5F9B1417)

  

অর্থাৎ, এখান থেকে আমরা একটা লিনিয়ার রিলেশন পেতে পারিঃ $inv_{n-1} \space (mod \space m) \equiv inv_n \times n \space (mod \space m),$ যেখানে $inv_n$ হচ্ছে $m$ এর সাপেক্ষে $n!$ এর মডুলার ইনভার্স। এই রিলেশন কাজে লাগিয়ে আমরা খুব সহজেই $(n-1)$ থেকে $1$ পর্যন্ত লুপ চালিয়ে $1!$ থেকে $n!$ পর্যন্ত সকল $i!$ এর মডুলার ইনভার্স $O(n)$ এ বের করতে পারি।

Total Complexity for Calculating Modular Inverse: $O(logm + n) \approx O(n)$
  


**প্রবলেম ২ঃ** দুটি সংখ্যা $b (b\neq m)$ এবং $n$ দেওয়া আছে । $b^1$ থেকে $b^n$ পর্যন্ত সবগুলো $b^i$ এর মডুলার ইনভার্স বের করতে হবে ।

**সলিউশনঃ** প্রত্যেকটি $b^i (mod \space m)$, bigmod ব্যবহার করে বের করে তারপর তাদের মডুলার ইনভার্স ক্যালুকুলেট করে অভারল $O(nlogm)$ এ এই প্রবলেম সলভ করা যায়। কিন্তু এই প্রবলেমও $O(n)$ এ সলভ করা সম্ভব । প্রথমে $b^n (mod \space m)$, bigmod ব্যবহার করে বের করব । এরপর এর মডুলার ইনভার্স বের করব। এখন,


![](https://scontent.fdac6-1.fna.fbcdn.net/v/t1.0-9/120258187_353818995818080_1578862520911070149_n.jpg?_nc_cat=101&_nc_sid=32a93c&_nc_ohc=wvswsZ_egBQAX_LRcG8&_nc_ht=scontent.fdac6-1.fna&oh=9822b29d2ee2e1afc2ea084621d3a756&oe=5F9AD6F7)


তাহলে, এখান থেকে এই লিনিয়ার রিলেশন পাওয়া যায়ঃ $inv_{n-1} \space (mod \space m) \equiv inv_n \times b \space (mod \space m)$, যেখানে, $inv_n$ হচ্ছে $m$ এর সাপেক্ষে $b^n$ এর মডুলার ইনভার্স । এই রিলেশন কাজে লাগিয়ে খুব সহজেই $(n-1)$ থেকে $1$ পর্যন্ত একটি লুপ চালিয়ে $b^1$ থেকে $b^n$ পর্যন্ত সবগুলো $b^i$ এর মডুলার ইনভার্স $O(n)$ এ বের করা সম্ভব ।
  
Total Complexity for Calculating Modular Inverse: $O(logm + n) \approx O(n)$
