# পাইথন বা অন্য কোনো ল্যাঙ্গুয়েজ দিয়ে ওয়ার্ডপ্রেস পোষ্ট করার সময়  REST API কেন ব্লক করে?
আমরা যারা পাইথন দিয়ে ওয়ার্ডপ্রেস সাইট এ অটোমেটিক পোস্ট করি বিভিন্ন সময় স্ট্যাটাস কোড ২০১ না এসে ৪০৬, ২০০ এধরণের এরর রিটার্ন করে ।
- নোট: পোষ্ট রিকোয়েস্ট এর জন্য ২০০ রিটার্ন আসলে সেটা এরর । রেস্ট API কোনো কিছু ক্রিয়েট করলে ২০১ রিটার্ন আসবে ।
## ১. বেসিক অথোরাইজেশন ঠিক আছে কিনা চেক করা ।
## ২. হোস্টিং এর MOD সিকিউরিটি বা ওয়ার্ডপ্রেসে কোনো সিকিউরিটি এনাবল আছে কিনা ।  
```MOD সিকিউরিটি ব্লক করলে, playload এ এভাবে পরিবর্তন আনলে ব্লক করবেনা ```
```py
import requests
import json
username = 'admin'
password = 'xxx xxx xxx xx xxx xxx'  # application pass
url = 'https://domain.com/wp-json/wp/v2/posts'
post_data = {
    "title": "Test Job",
    "content": "Test content",
    "status": "publish"
}
json_data = json.dumps(post_data)

response = requests.post(
    url,
    headers={
        'Content-Type': 'application/json',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3'
    },
    data=json_data,
    auth=(username, password)
)

if response.status_code == 201:
    print("Job post created successfully.")
    print("Response data:", response.json())
else:
    print("Failed to create job post. Status code:", response.status_code)

```
সিপ্যানেল হোস্টিং এ MOD সিকিউরিটি অপশন পেয়ে যাবে । বা হোস্টিং এর কাস্টমার সাপোর্ট এ কথা বলেন ।
## ৩. https ঠিক আছে কিনা, যদি WWW থাকলে URL এর সাথে WWW. অ্যাড করতে হবে (এর জন্য ২০০ রিটার্ন করতে পারে )
## ৪. PHP ৭.৪ ভার্সন সিলেক্ট করতে পারেন ।
## ৫. অনেক ওয়ার্ডপ্রেস সাইট বট ব্লক করে । requests লাইব্রেরি পরিবর্তে cloudscraper লাইব্রেরি দিয়ে পোষ্ট রিকোয়েস্ট দেন ।
## ৬. অথর, ক্যাটেগরি, ট্যাগ, ফিচার ইমেজ, ডিসএবল করে চেক করতে পারেন ।
## ৭. কিছু কিছু সাইট এ cloudscraper ব্যবহার করলে SSL এরর আসতে পারে 
## ৮. রেস্ট API এন্ড পয়েন্ট আলাদা হতে পারে । (ওয়ার্ডপ্রেস পার্মালিংক থেকে ফিক্স করতে হবে )

আমার নলেজে এগুলা আছে । কন্ট্রিবিউট করতে পারেন এর বাইরে কিছু থাকলে ।
