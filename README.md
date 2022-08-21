# পাইথন বা অন্য কোনো ল্যাঙ্গুয়েজ দিয়ে ওয়ার্ডপ্রেস পোষ্ট করার সময়  REST API কেন ব্লক করে?
আমরা যারা পাইথন দিয়ে ওয়ার্ডপ্রেস সাইট এ অটোমেটিক পোস্ট করি বিভিন্ন সময় স্ট্যাটাস কোড ২০১ না এসে ৪০৬, ২০০ এধরণের এরর রিটার্ন করে ।
নোট: পোষ্ট রিকোয়েস্ট এর জন্য ২০০ রিটার্ন আসলে সেটা এরর । (গতকাল পর্যন্ত ২০০, ২০১ সেম মনে করতাম, কিন্তু আউয়াল ভাইয়ের থেকে জানতে পারলাম ২ টা আলাদা ।)
## ১. বেসিক অথোরাইজেশন ঠিক আছে কিনা চেক করা ।
## ২. হোস্টিং এর MOD সিকিউরিটি বা ওয়ার্ডপ্রেসে কোনো সিকিউরিটি এনাবল আছে কিনা । 
সিপ্যানেল হোস্টিং এ MOD সিকিউরিটি অপশন পেয়ে যাবে । বা হোস্টিং এর কাস্টমার সাপোর্ট এ কথা বলেন ।
## ৩. https ঠিক আছে কিনা, যদি www থাকলে বাদ দেন (এর জন্য ২০০ রিটার্ন করতে পারে )
## ৪. PHP ৭.৪ ভার্সন সিলেক্ট করতে পারেন ।
## ৫. .htaccess ফাইল এ, আপডেট:
Most shared hosts have disabled the HTTP Authorization Header by default.
To enable this option you’ll need to edit your .htaccess file by adding the following:
RewriteCond %{HTTP:Authorization} ^(.*)
RewriteRule ^(.*) - [E=HTTP_AUTHORIZATION:%1]

আমার নলেজে এগুলা আছে । কমেন্ট করতে পারেন এর বাইরে কিছু থাকলে ।
