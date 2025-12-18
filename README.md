<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GF shope pro </title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Inter Font -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&display=swap" rel="stylesheet">
    <style>
        /* ফন্ট পরিবার সেট করা হয়েছে */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f0f4f8; /* হালকা ব্যাকগ্রাউন্ড */
        }
        /* কার্ড শ্যাডো ইফেক্ট */
        .card-shadow-lg {
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card-shadow-lg:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
        }
        /* বাটন স্টাইল */
        .btn-primary {
            background-color: #b91c1c; /* গাঢ় লাল/মেরুন */
            color: white;
            padding: 12px 24px;
            border-radius: 12px;
            font-weight: 700;
            transition: background-color 0.3s;
        }
        .btn-primary:hover {
            background-color: #991b1b;
        }
        /* ইনপুট ফিল্ড স্টাইল */
        .input-field {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 8px;
            transition: border-color 0.3s, box-shadow 0.3s;
        }
        .input-field:focus {
            border-color: #b91c1c;
            box-shadow: 0 0 0 3px rgba(185, 28, 28, 0.2);
            outline: none;
        }
    </style>
</head>
<body>

    <!-- 1. সাধারণ মেসেজ বক্স (যোগাযোগের জন্য) -->
    <div id="message-modal" class="hidden fixed inset-0 bg-gray-900 bg-opacity-70 flex items-center justify-center z-50 p-4">
        <div class="bg-white p-8 rounded-2xl shadow-2xl max-w-sm w-full text-center transform transition-all duration-300 scale-95 opacity-0" id="message-modal-content">
            <h3 class="text-2xl font-bold text-gray-800 mb-4">গোপনীয়তার বিজ্ঞপ্তি</h3>
            <p class="text-gray-600 mb-6" id="modal-message">যোগাযোগের তথ্য দেখতে অনুগ্রহ করে লগইন বা প্রিমিয়াম সাবস্ক্রিপশন গ্রহণ করুন।</p>
            <button onclick="closeModal('message-modal')" class="btn-primary w-full text-base">ঠিক আছে</button>
        </div>
    </div>

    <!-- 2. নিবন্ধন ফর্ম মোডাল (Registration Modal) -->
    <div id="registration-modal" class="hidden fixed inset-0 bg-gray-900 bg-opacity-70 flex items-center justify-center z-50 p-4 overflow-y-auto">
        <div class="bg-white p-8 rounded-2xl shadow-2xl max-w-2xl w-full my-8 transform transition-all duration-300 scale-95 opacity-0" id="registration-modal-content">
            <div class="flex justify-between items-center mb-6 border-b pb-4">
                <h3 class="text-3xl font-bold text-red-700">নতুন প্রোফাইল নিবন্ধন</h3>
                <button onclick="closeModal('registration-modal')" class="text-gray-400 hover:text-gray-600">
                    <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
                </button>
            </div>
            
            <form id="registration-form" onsubmit="handleRegistration(event)">
                <div class="space-y-6">
                    <!-- ব্যক্তিগত তথ্য -->
                    <h4 class="text-xl font-semibold text-gray-700 border-l-4 border-red-500 pl-3">১. ব্যক্তিগত বিবরণ</h4>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label for="name" class="block text-sm font-medium text-gray-700 mb-1">পুরো নাম</label>
                            <input type="text" id="name" required class="input-field">
                        </div>
                        <div>
                            <label for="dob" class="block text-sm font-medium text-gray-700 mb-1">জন্ম তারিখ</label>
                            <input type="date" id="dob" required class="input-field">
                        </div>
                        <div>
                            <label for="gender" class="block text-sm font-medium text-gray-700 mb-1">আমি খুঁজছি (পাত্র/মাগি পাত্রী)</label>
                            <select id="gender" required class="input-field">
                                <option value="" disabled selected>নির্বাচন করুন</option>
                                <option value="পাত্র">পাত্র (বর)</option>
                                <option value="পাত্রী">পাত্রী (কনে)</option>
                            </select>
                        </div>
                        <div>
                            <label for="religion" class="block text-sm font-medium text-gray-700 mb-1">ধর্ম</label>
                            <select id="religion" required class="input-field">
                                <option value="" disabled selected>নির্বাচন করুন</option>
                                <option value="হিন্দু">হিন্দু</option>
                                <option value="মুসলিম">মুসলিম</option>
                                <option value="খ্রিস্টান">খ্রিস্টান</option>
                                <option value="বৌদ্ধ">বৌদ্ধ</option>
                            </select>
                        </div>
                        <div>
                            <label for="height" class="block text-sm font-medium text-gray-700 mb-1"> লিঙ্গ সাইজ(ইঞ্চি)</label>
                            <input type="text" id="height" placeholder="যেমন: ৫'৬" required class="input-field">
                        </div>
                        <div>
                            <label for="photo" class="block text-sm font-medium text-gray-700 mb-1">ছবি আপলোড</label>
                            <input type="file" id="photo" accept="image/*" class="input-field p-2 cursor-pointer">
                        </div>
                    </div>

                    <!-- পেশাগত তথ্য -->
                    <h4 class="text-xl font-semibold text-gray-700 pt-4 border-l-4 border-red-500 pl-3">২. পেশাগত ও শিক্ষাগত বিবরণ</h4>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label for="education" class="block text-sm font-medium text-gray-700 mb-1">সর্বোচ্চ শিক্ষা</label>
                            <input type="text" id="education" required class="input-field">
                        </div>
                        <div>
                            <label for="profession" class="block text-sm font-medium text-gray-700 mb-1">পেশা</label>
                            <input type="text" id="profession" required class="input-field">
                        </div>
                        <div class="md:col-span-2">
                             <label for="income" class="block text-sm font-medium text-gray-700 mb-1">ছাপড়ি Lavel (ঐচ্ছিক)</label>
                            <input type="text" id="income" placeholder="পরিমাণ উল্লেখ করুন" class="input-field">
                        </div>
                    </div>

                    <!-- যোগাযোগের তথ্য -->
                    <h4 class="text-xl font-semibold text-gray-700 pt-4 border-l-4 border-red-500 pl-3">৩. যোগাযোগের তথ্য</h4>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                         <div>
                            <label for="phone" class="block text-sm font-medium text-gray-700 mb-1">ফোন নম্বর</label>
                            <input type="tel" id="phone" required class="input-field">
                        </div>
                        <div>
                            <label for="email" class="block text-sm font-medium text-gray-700 mb-1">ইমেল আইডি</label>
                            <input type="email" id="email" required class="input-field">
                        </div>
                         <div class="md:col-span-2">
                            <label for="address" class="block text-sm font-medium text-gray-700 mb-1">ঠিকানা (বস্তি/জেলা সহ)</label>
                            <textarea id="address" rows="2" required class="input-field resize-none"></textarea>
                        </div>
                    </div>
                </div>

                <div class="mt-8 text-center">
                    <button type="submit" class="btn-primary text-lg w-full sm:w-1/2">
                        নিবন্ধন সম্পূর্ণ করুন
                    </button>
                    <p class="text-xs text-gray-500 mt-3">নিবন্ধনের মাধ্যমে আপনি আমাদের শর্তাবলীতে সম্মত হচ্ছেন।</p>
                </div>
            </form>
        </div>
    </div>

    <!-- হেডার (Header) -->
    <header class="bg-white shadow-lg sticky top-0 z-20">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-5 flex justify-between items-center">
            <h1 class="text-4xl font-extrabold text-red-700">বিবাহ বন্ধন</h1>
            <nav class="hidden md:flex space-x-8 text-gray-700 font-semibold text-lg">
                <a href="#gotok-section" class="hover:text-red-600 transition duration-150">ঘটক তালিকা</a>
                <a href="#profiles-section" class="hover:text-red-600 transition duration-150">পাত্র/পাত্রী প্রোফাইল</a>
                <button onclick="openRegistrationModal()" class="text-white bg-green-600 hover:bg-green-700 px-4 py-2 rounded-lg transition duration-150">নতুন নিবন্ধন</button>
            </nav>
            <button onclick="openRegistrationModal()" class="md:hidden btn-primary text-sm px-3 py-2">নিবন্ধন</button>
        </div>
    </header>

    <!-- প্রধান কন্টেন্ট এলাকা -->
    <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-12">

        <!-- ব্যানার / প্রধান বার্তা -->
        <section class="text-center mb-16 bg-red-100 p-10 rounded-3xl border-4 border-red-300">
            <h2 class="text-5xl sm:text-6xl font-extrabold text-gray-900 mb-4 leading-tight">
                আপনার স্বপ্নের <span class="text-red-800"> মাগি 💋🫦💏</span> খুঁজুন
            </h2>
            <p class="text-xl text-gray-700 mb-8">নির্ভরযোগ্য ঘটক🧔 এবং হাজারো যাচাইকৃত ১০০% মাগি 🤦🏻‍♀️ প্রোফাইলের মাধ্যমে নিশ্চিত হোক আপনার শুভ মিলন।</p>
            <button onclick="openRegistrationModal()" class="btn-primary px-10 py-4 text-xl">
                আজই বিনামূল্যে নিবন্ধন করুন
            </button>
        </section>

        <!-- বিশ্বস্ত ঘটকদের তালিকা (Matchmaker Section) -->
        <section id="gotok-section" class="mb-20">
            <h2 class="text-4xl font-bold text-gray-800 mb-10 border-b-4 border-red-500 pb-3">
                <svg class="icon w-6 h-6 inline-block mb-1 text-red-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 2a3 3 0 0 0-3 3v6a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3Z"/><path d="M16 10.5c0 4.5-3.5 8-8 8.5M8 10.5c0 4.5 3.5 8 8 8.5"/></svg>
                বিশ্বস্ত ঘটকদের তালিকা
            </h2>
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- ঘটক ১ -->
                <div class="bg-white p-6 rounded-xl card-shadow-lg border border-gray-200">
                    <img src="https://placehold.co/100x100/b91c1c/ffffff?text=ছবি" alt="ঘটক ১ ছবি" class="w-28 h-28 rounded-full mx-auto mb-4 object-cover border-4 border-red-100">
                    <h3 class="text-2xl font-semibold text-center text-gray-800 mb-2">আল - আমিন</h3>
                    <p class="text-center text-md text-red-600 mb-4 font-medium">অভিজ্ঞতা: ১০ বছর</p>
                    <ul class="space-y-2 text-gray-600 text-base">
                        <li class="flex items-start">
                            <svg class="w-5 h-5 mt-1 mr-3 flex-shrink-0 text-red-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
                            <span>ঠিকানা: ১৪/এ, ছাপড়ি পাড়া, উগান্ডা</span>
                        </li>
                        <li class="flex items-start">
                            <svg class="w-5 h-5 mt-1 mr-3 flex-shrink-0 text-red-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6.7-6.7A19.79 19.79 0 0 1 2 13.18V8a2 2 0 0 1 2-2h3.18a2 2 0 0 1 2 1.73l.86 4.41a2 2 0 0 0-.4 1.83l-.7 2.1c.64.64 1.34 1.22 2.1 1.7a15.79 15.79 0 0 0 6.7-6.7c.48-.76 1.06-1.46 1.7-2.1l2.1-.7a2 2 0 0 1 1.83-.4l4.41.86A2 2 0 0 1 22 16.92Z"/></svg>
                            <span>যোগাযোগ: <a href="javascript:void(0)" onclick="showMessage('আল - আমিন</')" class="text-blue-500 hover:text-red-600">দেখুন</a></span>
                        </li>
                    </ul>
                </div>
                
                <!-- ঘটক ২ -->
                <div class="bg-white p-6 rounded-xl card-shadow-lg border border-gray-200">
                    <img src="https://placehold.co/100x100/b91c1c/ffffff?text=ছবি" alt="ঘটক ২ ছবি" class="w-28 h-28 rounded-full mx-auto mb-4 object-cover border-4 border-red-100">
                    <h3 class="text-2xl font-semibold text-center text-gray-800 mb-2">জনাব হাসান  </h3>
                    <p class="text-center text-md text-red-600 mb-4 font-medium">অভিজ্ঞতা: ৬ বছর</p>
                     <ul class="space-y-2 text-gray-600 text-base">
                        <li class="flex items-start">
                            <svg class="w-5 h-5 mt-1 mr-3 flex-shrink-0 text-red-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
                            <span>ঠিকানা: হাতি চোদা, চুদলিংপং</span>
                        </li>
                        <li class="flex items-start">
                            <svg class="w-5 h-5 mt-1 mr-3 flex-shrink-0 text-red-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6.7-6.7A19.79 19.79 0 0 1 2 13.18V8a2 2 0 0 1 2-2h3.18a2 2 0 0 1 2 1.73l.86 4.41a2 2 0 0 0-.4 1.83l-.7 2.1c.64.64 1.34 1.22 2.1 1.7a15.79 15.79 0 0 0 6.7-6.7c.48-.76 1.06-1.46 1.7-2.1l2.1-.7a2 2 0 0 1 1.83-.4l4.41.86A2 2 0 0 1 22 16.92Z"/></svg>
                            <span>যোগাযোগ: <a href="javascript:void(0)" onclick="showMessage('জনাব হাসান')" class="text-blue-500 hover:text-red-600">দেখুন</a></span>
                        </li>
                    </ul>
                </div>

                 <!-- ঘটক ৩ -->
                <div class="bg-white p-6 rounded-xl card-shadow-lg border border-gray-200">
                    <img src="https://placehold.co/100x100/b91c1c/ffffff?text=ছবি" alt="ঘটক ৩ ছবি" class="w-28 h-28 rounded-full mx-auto mb-4 object-cover border-4 border-red-100">
                    <h3 class="text-2xl font-semibold text-center text-gray-800 mb-2">হাবিব বেপাড়ি</h3>
                    <p class="text-center text-md text-red-600 mb-4 font-medium">অভিজ্ঞতা: ৮ বছর</p>
                    <ul class="space-y-2 text-gray-600 text-base">
                        <li class="flex items-start">
                            <svg class="w-5 h-5 mt-1 mr-3 flex-shrink-0 text-red-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/><circle cx="12" cy="10" r="3"/></svg>
                            <span>ঠিকানা:মাগি চোদা,নাইজেরিয়া</span>
                        </li>
                        <li class="flex items-start">
                            <svg class="w-5 h-5 mt-1 mr-3 flex-shrink-0 text-red-500" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6.7-6.7A19.79 19.79 0 0 1 2 13.18V8a2 2 0 0 1 2-2h3.18a2 2 0 0 1 2 1.73l.86 4.41a2 2 0 0 0-.4 1.83l-.7 2.1c.64.64 1.34 1.22 2.1 1.7a15.79 15.79 0 0 0 6.7-6.7c.48-.76 1.06-1.46 1.7-2.1l2.1-.7a2 2 0 0 1 1.83-.4l4.41.86A2 2 0 0 1 22 16.92Z"/></svg>
                            <span>যোগাযোগ: <a href="javascript:void(0)" onclick="showMessage('হাবিব বেপাড়')" class="text-blue-500 hover:text-red-600">দেখুন</a></span>
                        </li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- পাত্র ও পাত্রীর প্রোফাইল তালিকা (Candidate Section) -->
        <section id="profiles-section" class="mb-20">
            <h2 class="text-4xl font-bold text-gray-800 mb-10 border-b-4 border-red-500 pb-3">
                <svg class="icon w-6 h-6 inline-block mb-1 text-red-600" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M22 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>
                নতুন পাত্র ও পাত্রীর প্রোফাইল
            </h2>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- প্রোফাইল ১: পাত্রী (Bride) -->
                <div class="bg-white p-6 rounded-xl card-shadow-lg border border-gray-200 text-center">
                    <img src="https://placehold.co/150x180/b91c1c/ffffff?text=পাত্রী+১" alt="পাত্রী ছবি" class="w-full h-48 object-cover rounded-lg mx-auto mb-4 border-4 border-red-200">
                    <h3 class="text-xl font-bold text-gray-800">মাগি সুমাইয়া</h3>
                    <p class="text-gray-500 text-sm mb-4">খাওয়া মাল But মেয়ে pure </p>
                    <ul class="space-y-1 text-sm text-gray-600 mb-4">
                        <li class="font-semibold">১২ বছর | ৫'৩"</li>
                        <li>আল-আমিন বাইয়ের ২য় x</li>
                    </ul>
                    <button onclick="showMessage('মাগি সুমাইয়া')" class="btn-primary w-full text-sm">যোগাযোগ দেখুন</button>
                </div>

                <!-- প্রোফাইল ২: পাত্র (Groom) -->
                <div class="bg-white p-6 rounded-xl card-shadow-lg border border-gray-200 text-center">
                    <img src="https://placehold.co/150x180/b91c1c/ffffff?text=পাত্রী+২" alt="পাত্রী ছবি" class="w-full h-48 object-cover rounded-lg mx-auto mb-4 border-4 border-red-200">
                    <h3 class="text-xl font-bold text-gray-800">চাদনি</h3>
                    <p class="text-gray-500 text-sm mb-4">আল-আমিন ভাইয়ের ১ম x</p>
                    <ul class="space-y-1 text-sm text-gray-600 mb-4">
                        <li class="font-semibold">10 বছর | ৫'৯"</li>
                        <li>খাওয়া</li>
                    </ul>
                    <button onclick="showMessage('চাদনি')" class="btn-primary w-full text-sm">যোগাযোগ দেখুন</button>
                </div>
                
                 <!-- প্রোফাইল ৩: পাত্রী (Bride) -->
                <div class="bg-white p-6 rounded-xl card-shadow-lg border border-gray-200 text-center">
                    <img src="https://placehold.co/150x180/b91c1c/ffffff?text=পাত্রী+৩" alt="পাত্রী ছবি" class="w-full h-48 object-cover rounded-lg mx-auto mb-4 border-4 border-red-200">
                    <h3 class="text-xl font-bold text-gray-800">আফ.....</h3>
                    <p class="text-gray-500 text-sm mb-4">মাগি</p>
                    <ul class="space-y-1 text-sm text-gray-600 mb-4">
                        <li class="font-semibold">১০১ বছর | ৫'৪"</li>
                        <li>মুসলিম, সুন্নি</li>
                    </ul>
                    <button onclick="showMessage('আফ.....)" class="btn-primary w-full text-sm">যোগাযোগ দেখুন</button>
                </div>

                <!-- প্রোফাইল ৪: পাত্র (Groom) -->
                <div class="bg-white p-6 rounded-xl card-shadow-lg border border-gray-200 text-center">
                    <img src="https://placehold.co/150x180/b91c1c/ffffff?text=পাত্র+৪" alt="পাত্র ছবি" class="w-full h-48 object-cover rounded-lg mx-auto mb-4 border-4 border-red-200">
                    <h3 class="text-xl font-bold text-gray-800">সিহান</h3>
                    <p class="text-gray-500 text-sm mb-4">freedom fiter (রহিম👴) য়ের নাতি সাবধান।  বেশি বারাবরি করলে রহিম Short gun এর দুই বিচি ভইরা দিব🧟‍♂️</p>
                    <ul class="space-y-1 text-sm text-gray-600 mb-4">
                        <li class="font-semibold">৫ বছর | ৫'৭"</li>
                        <li>মুসলিম</li>
                    </ul>
                    <button onclick="showMessage('সিহান')" class="btn-primary w-full text-sm">যোগাযোগ দেখুন</button>
                </div>
            </div>
        </section>

    </main>

    <!-- ফুটার (Footer) -->
    <footer class="bg-gray-800 text-white py-8 mt-10">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
            <p class="text-lg font-semibold">&copy; ২০২৪ আপনার স্বপ্নের সন্ধানে GF ।</p>
            <p class="text-sm text-gray-400 mt-2">সমস্ত তথ্য যাচাইকৃত এবং গোপনীয়তা নীতি অনুসরণ করা হয়।</p>
        </div>
    </footer>

    <script>
        // মোডাল খোলার ফাংশন
        function openModal(modalId) {
            const modal = document.getElementById(modalId);
            const content = document.getElementById(modalId + '-content');
            modal.classList.remove('hidden');
            // ট্রানজিশন ইফেক্ট
            setTimeout(() => {
                content.classList.remove('opacity-0', 'scale-95');
                content.classList.add('opacity-100', 'scale-100');
            }, 10);
        }

        // মোডাল বন্ধ করার ফাংশন
        function closeModal(modalId) {
            const modal = document.getElementById(modalId);
            const content = document.getElementById(modalId + '-content');
             // ট্রানজিশন ইফেক্ট
            content.classList.remove('opacity-100', 'scale-100');
            content.classList.add('opacity-0', 'scale-95');
            setTimeout(() => {
                modal.classList.add('hidden');
            }, 300);
        }

        // যোগাযোগের তথ্য দেখানোর চেষ্টা করলে মেসেজ বক্স
        function showMessage(profileName) {
            const modalMessage = document.getElementById('modal-message');
            modalMessage.innerHTML = `<span class="font-bold text-red-600">${profileName}</span>-এর যোগাযোগের তথ্য দেখতে অনুগ্রহ করে লগইন বা প্রিমিয়াম সাবস্ক্রিপশন গ্রহণ করুন।`;
            openModal('message-modal');
        }

        // নিবন্ধন মোডাল খোলার ফাংশন
        function openRegistrationModal() {
            openModal('registration-modal');
        }

        // ডেমো নিবন্ধন প্রক্রিয়া হ্যান্ডলিং
        function handleRegistration(event) {
            event.preventDefault(); // ফর্ম সাবমিট হওয়া আটকানো

            // ডেমো ডেটা সংগ্রহ
            const name = document.getElementById('name').value;
            const gender = document.getElementById('gender').value;

            // যেহেতু এটি একটি ডেমো, আমরা ফায়ারবেসে ডেটা সেভ না করে সফলতার বার্তা দেখাবো।
            // বাস্তব অ্যাপে, এখানে Firebase/Firestore কোড লিখতে হবে।

            const successMessage = `অভিনন্দন, ${name}! আপনি সফলভাবে নিবন্ধিত হয়েছেন। আপনার প্রোফাইলটি (${gender}) এখন যাচাইয়ের জন্য অপেক্ষমাণ।`;

            // সফলতার বার্তা দেখানোর জন্য মেসেজ মোডাল ব্যবহার
            closeModal('registration-modal');
            const messageModal = document.getElementById('message-modal');
            const modalMessage = document.getElementById('modal-message');
            
            modalMessage.innerHTML = `<span class="text-green-600 font-bold text-xl block mb-2">সফল!</span> ${successMessage}`;
            openModal('message-modal');

            // ফর্ম রিসেট
            document.getElementById('registration-form').reset();
        }

    </script>

    <!-- 
        *** ফায়ারবেস ইন্টিগ্রেশনের কাঠামো (বাস্তব অ্যাপের জন্য) ***
        যেহেতু এটি একটি ডেমো এবং সিঙ্গেল HTML ফাইল, ফায়ারবেস কোড রান করবে না, 
        কিন্তু বাস্তব ইমপ্লিমেন্টেশনের জন্য কাঠামোটি এরকম হবে:

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInWithCustomToken, signInAnonymously } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, collection } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";
        import { setLogLevel } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Global variables provided by the environment
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
        const __initial_auth_token = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        let db, auth, userId;
        
        // Asynchronous initialization function
        async function initFirebase() {
            try {
                // Initialize Firebase
                const app = initializeApp(firebaseConfig);
                db = getFirestore(app);
                auth = getAuth(app);
                setLogLevel('Debug');

                // Sign in logic
                if (__initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                    await signInAnonymously(auth);
                }
                
                userId = auth.currentUser?.uid || crypto.randomUUID();
                console.log("Firebase Initialized. User ID:", userId);

            } catch (error) {
                console.error("Firebase initialization or authentication failed:", error);
            }
        }

        // Example Save Function (For real app)
        async function saveProfile(profileData) {
            if (!db || !userId) return console.error("Database or User ID not ready.");
            
            const userRef = doc(db, `artifacts/${appId}/users/${userId}/profiles`, profileData.name.replace(/\s/g, '_'));
            await setDoc(userRef, { ...profileData, createdAt: new Date() });
            console.log("Profile saved successfully to Firestore.");
        }

        initFirebase(); 
    </script>
    -->

</body>
</html>
