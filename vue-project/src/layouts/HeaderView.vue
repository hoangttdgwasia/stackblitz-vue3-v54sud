<script>

</script>
<template>
    <header class="flex justify-center py-12 items-center">
        <div class="container flex justify-between align-middle items-center">
            <div class="logo">
                <a href="#">
                    <img src="/images/logo-bookmark.svg" alt="">
                </a>
            </div>
            <nav class="flex">
                <ul class="space-x-10 font-theme-heading font-medium items-center hidden md:flex flex-col space-y-7 md:space-y-0 md:flex-row">
                    <li class="uppercase hover:text-theme-secondary transition duration-200">
                        <a href="#todo">Todo App</a>
                    </li>
                    <li class="uppercase hover:text-theme-secondary transition duration-200">
                        <a href="#">FAQ</a>
                    </li>
                    <li class="uppercase hover:text-theme-secondary transition duration-200">
                        <a href="#">Subscribe</a>
                    </li>
                    <li class="uppercase bg-theme-secondary px-6 py-2 text-white rounded shadow-md hover:bg-white border-2 border-transparent hover:border-theme-secondary hover:text-theme-secondary cursor-pointer transition duration-200">
                        <a href="#">Download</a>
                    </li>
                </ul>
            </nav>
        </div>
    </header>
</template>