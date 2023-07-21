<template>
  <div class="flex flex-col justify-between p-8 h-[100vh] bg-cyan-950 overflow-auto">
    <div class="mb-4">
      <header>
        <h1 class="text-slate-400 text-center tracking-wider mb-6">
          <img
            src="/logo.svg"
            alt="Planny logo"
            width="120"
            class="mx-auto mb-2"
          >
          Your plannig board
        </h1>
      </header>
      <main>
        <KanbanBoard />
      </main>
    </div>
    <footer class="text-center text-slate-400">
      Press Ctrl and move <span class="font-bold">column</span> to dublicate<br>
      Select <span class="font-bold">task</span> and press Backspace to delete
    </footer>
  </div>
</template>

<style>
::-webkit-scrollbar {
    width: 10px;
    height: 10px;
}
  
::-webkit-scrollbar-track {
    background: #084258;
    border-radius: 50px;
}
  
::-webkit-scrollbar-thumb {
    background: #072936;
    border-radius: 50px;
}
  
::-webkit-scrollbar-thumb:hover {
    background: rgb(6, 36, 49);
}
</style>
