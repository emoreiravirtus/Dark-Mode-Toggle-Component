<template>
  <label class="label">
  <div class="toggle">
    <input class="toggle-state" type="checkbox" name="check" value="check" />
    <div class="indicator"><i class="fas fa-moon"></i><i class="fas fa-sun"></i></div>
  </div>
</label>
</template>

<script>
export default {
    data() {
        return {
            active: true
        }
    },
    mounted(){
        
        const toggleSwitch = document.querySelector('input[type="checkbox"]');

        const switchTheme = e => {
            if (e.target.checked) {
                document.documentElement.setAttribute('data-theme', 'dark');
                localStorage.setItem('theme', 'dark'); //add this
            }
            else {
                document.documentElement.setAttribute('data-theme', 'light');
                localStorage.setItem('theme', 'light'); //add this
            }   
        }

        toggleSwitch.addEventListener('change', switchTheme, false);

        const currentTheme = localStorage.getItem('theme') ? localStorage.getItem('theme') : null;

        if (currentTheme) {
            document.documentElement.setAttribute('data-theme', currentTheme);

            if (currentTheme === 'dark') {
                toggleSwitch.checked = true;
            }
        }
        
    }
}
</script>

<style>

:root {
    --primary-color: #302AE6;
    --secondary-color: #536390;
    --font-color: #424242;
    --bg-color: rgb(230, 230, 230);
    --heading-color: #292922;
}

[data-theme="dark"] {
    --primary-color: #9A97F3;
    --secondary-color: #818cab;
    --font-color: #e1e1ff;
    --bg-color: #161625;
    --heading-color: #818cab;
}

.label {
  display: inline-flex !important;
  align-items: center;
  cursor: pointer;
  color: #394a56;
  margin-right: 0.3rem;
}

.label-text {
  margin-left: 16px;
}

.toggle {
  isolation: isolate;
  position: relative;
  height: 30px;
  width: 60px;
  border-radius: 15px;
  overflow: hidden;
  border: 1px solid #48546a;
}

.toggle-state {
  display: none;
}

.indicator {
  height: 100%;
  width: 200%;
  background: var(--bg-color);
  border-radius: 15px;
  transform: translate3d(-75%, 0, 0);
  transition: transform 0.4s cubic-bezier(0.85, 0.05, 0.18, 1.35);
  position: relative;
  align-items: center;
  display: inline-flex;
  color: var(--font-color)
}

.indicator .fa-moon{
    position: absolute;
    left: 0.5rem;
}

.indicator .fa-sun{
    position: absolute;
    right: 0.5rem;
}

.toggle-state:checked ~ .indicator {
  transform: translate3d(25%, 0, 0);
}
</style>
