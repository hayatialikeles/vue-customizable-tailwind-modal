# VUE JS CUSTOMİZABLE TAILWIND MODAL

customizable tailwind modal is a vue.js library.

## Installation

Use the package manager npm to install .

```bash
npm i vue-customizable-tailwind-modal
```

## Usage

```javascript
import modal from vue-customizable-tailwind-modal

componentes:{
   modal
},

  <modal 
        @closed="this event is modal closed  trigger"
        @opened="this event is modal opened trigger"
        toggleBtnClass="w-full rounded p-2"
        containerClass="w-6/12  shadow h-80 bg-gray-200 relative rounded"
        title="Modal title"
        headerContainerClass="flex justify-between card-header p-4 border-b border-opacity-50 border-black"
        closeBtnClass="w-6 h-6 text-black"
        bodyContainerClass="p-4"
        footerClass=""
    >

        <template v-slot:open-btn-slot>
            Open Modal
        </template> 
        <template v-slot:header>
            <div :class="headerContainerClass">
                <h5>{{ title }}</h5>
                <button @click="closeModal(true)" :class="closeBtnClass">X</button>
            </div>
        </template>
    
        modal content detail

        <template v-slot:footer>
            Open Modal
        </template>
    </modal>


```
## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
Please make sure to update tests as appropriate.

## License
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

