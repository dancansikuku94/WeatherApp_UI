<template>
  <div>
    <div
      class="h-4 w-9 text-black font-sans bg-white justify-items-center pt-6 ml-5"
    >
      <input
        class="placeholder-gray-500 mx-auto p-6 pt-2 px-4 rounded-md flex-row placeholder-opacity-100  focus:bg-gray-50..."
        placeholder="Search..."
      />
    </div>
    </div>
    <!--<div class="flex-center ml-20 h-10 w-48 p-5">
  <img src="./src/assets/map.jpg" alt="" class="absolute inset-0 w-full h-full object-cover" />
  </div>-->
  <div class="pt-10">
<img src="/map.jpg" alt=""/>
  </div>
  <div class="bg-white pt-2">
      <h1 class="text-black text-xl text-bold pt-4 ml-5 font-ubuntu">Mulot Police Post</h1>
      <h2 class="text-black-500 text-xs ml-5 font-ubuntu">Weather forecast.</h2>
      <h3 class="text-black-500 text-sm ml-5 font-ubuntu">Today 3rd-June 2021</h3>
    </div>
    <div class="flex flex-row bg-white w-10">
      <div class="bg-white pt-4">
        <h1 class="text-black font-medium justify-items-center ml-10">
          Temperature.
        </h1>
        <div class="pt-6 h-5 w-4 flex-auto flex space-x-3">
          <div class="flex-auto flex-items-center">
            <h2 class="text-blue-600 font-bold">28*C</h2>
            <p class="text-black font-normal">Maximum</p>
          </div>
          <div class="flex-auto flex-items-center">
            <h3 class="text-blue-600 font-bold">17*C</h3>
            <p class="text-black font-normal">Minimum</p>
          </div>
        </div>
      </div>
      <div class="font-medium ml-10 pt-4">
        <h1 class="text-black font-medium">Additional Parameters</h1> 
        <p class="text-blue font-normal">Wind   24</p>
        <p class="text-blue font-normal">Pressure  45</p>
        <p class="text-blue font-normal">Precipitation 55</p>
        </div>
    </div>
<div class="flex flex-row bg-gray-50 pt-4 h-4 w-10">
  <div class="text-black">
   <p class="text-black font-normal">Tuesday</p>
  <img src="/sun.png" alt="" class="w=4/12 h=1/60"/>
   <p class="text-black font-light">Sunny Interval.</p>
    </div>
  <div class="text-black ml-10">
     <p class="text-black font-normal">Wednesday</p>
     <img src="/cloud.png" alt="" class="w-4/12 h-6/12" />
   <p class="text-black font-light">Sunny Interval.</p>
    </div>
  <div class="text-black ml-10">
     <p class="text-black font-normal">Thursday</p>
     <img src="/rain.jpg" alt="" class="w-4/12 h-6/12" />
   <p class="text-black font-light">Heavy Rain.</p>
  </div>
</div>
</template>



