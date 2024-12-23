<template>
  <div class="container-fluid">
    <div class="container">
      <!-- All Modal Here -->
      <columnCountModalComponent @update-url="updateUrlData"></columnCountModalComponent>
      <!-- First Section -->
      <section class="p-0 m-0 mt-3">
        <div class="d-flex flex-column w-100">
          <textarea ref="textarea" class="form-control" v-model="url" placeholder="Insert URL here!" style="height: 100px;"></textarea>
          <div class="d-flex flex-row align-items-center gap-4 mt-3">
            <!-- Button '<' -->
            <button class="btn py-1 px-4 border-1 text-warning border-warning" @click="prevUrls()">
              <i class="bi bi-arrow-counterclockwise"></i>
            </button>
            <!-- Button '>' -->
            <button class="btn py-1 px-4 border-1 text-warning border-warning" @click="nextUrls()">
              <i class="bi bi-arrow-clockwise"></i>
            </button>
            <!-- Button 'Open' -->
            <a class="btn py-1 px-4 border-1 text-success border-success" target="_blank" :href="url">
              Open
            </a>
            <!-- Button 'Clear' -->
            <button class="btn py-1 px-4 border-1 text-danger border-danger" @click="clearUrlData()">
              Clear
            </button>
          </div>
        </div>
      </section>
      <!-- Second Section -->
      <section class="p-0 m-0 mt-3">
        <div class="d-flex flex-row align-items-center w-100 overflow-hidden px-0 mx-0 justify-content-between gap-4">
          <!-- Tombol Prev -->
          <button class="prev btn border-light border-1 px-4 py-1 m-0 d-flex flex-row align-items-center gap-2" :disabled="currentIndexSecondSection === 0"  style="transition: background-color 0.3s ease; cursor: pointer;" @click="moveSliderSecondSection('prev')">
            <i class="bi bi-caret-left"></i>  
            Prev
          </button>
          <!-- Slider yang dapat digeser -->
          <div class="w-100 h-100 m-0 p-0 overflow-hidden">
            <div class="d-flex flex-row gap-4" style="transition: transform 0.3s ease;" :style="{ transform: 'translateX(-' + (currentIndexSecondSection * 100) / blocksVisibleSecondSection + '%)' }">
              <button class="btn py-1 px-3 border-light border-1" style="text-wrap: nowrap;" v-for="(block, index) in blocksSecondSection" :key="index" type="button" data-bs-toggle="modal" :data-bs-target="block.column_modal_id">{{ block.name }}</button>
            </div>
          </div>
          <!-- Tombol Next -->
          <button class="next btn border-light border-1 px-4 py-1 m-0 d-flex flex-row align-items-center gap-2" :disabled="currentIndexSecondSection >= blocksSecondSection.length - blocksVisibleSecondSection" style="transition: background-color 0.3s ease; cursor: pointer;" @click="moveSliderSecondSection('next')">
            Next
            <i class="bi bi-caret-right"></i>
          </button>
        </div>
      </section>
      <!-- Third Section -->
      <section class="p-0 m-0 mt-3">
        <div class="d-flex flex-row align-items-center w-100 overflow-hidden px-0 mx-0 justify-content-between gap-4">
          <!-- Tombol Prev -->
          <button class="prev btn border-light border-1 px-4 py-1 m-0 d-flex flex-row align-items-center gap-2" :disabled="currentIndexThirdSection === 0"  style="transition: background-color 0.3s ease; cursor: pointer;" @click="moveSliderThirdSection('prev')">
            <i class="bi bi-caret-left"></i>  
            Prev
          </button>
          <!-- Slider yang dapat digeser -->
          <div class="w-100 h-100 m-0 p-0 overflow-hidden">
            <div class="d-flex flex-row gap-4" style="transition: transform 0.3s ease;" :style="{ transform: 'translateX(-' + (currentIndexThirdSection * 100) / blocksVisibleThirdSection + '%)' }">
              <button class="btn py-1 px-3 border-light border-1" style="text-wrap: nowrap;" v-for="(block, index) in blocksThirdSection" :key="index">{{ block }}</button>
            </div>
          </div>
          <!-- Tombol Next -->
          <button class="next btn border-light border-1 px-4 py-1 m-0 d-flex flex-row align-items-center gap-2" :disabled="currentIndexThirdSection >= blocksThirdSection.length - blocksVisibleThirdSection" style="transition: background-color 0.3s ease; cursor: pointer;" @click="moveSliderThirdSection('next')">
            Next
            <i class="bi bi-caret-right"></i>
          </button>
        </div>
      </section>
      <!-- Fourth Section -->
      <section class="p-0 m-0 mt-3">
        <div class="d-flex flex-row align-items-center w-100 overflow-hidden px-0 mx-0 justify-content-between gap-4">
          <!-- Tombol Prev -->
          <button class="prev btn border-light border-1 px-4 py-1 m-0 d-flex flex-row align-items-center gap-2" :disabled="currentIndexFourthSection === 0"  style="transition: background-color 0.3s ease; cursor: pointer;" @click="moveSliderFourthSection('prev')">
            <i class="bi bi-caret-left"></i>  
            Prev
          </button>
          <!-- Slider yang dapat digeser -->
          <div class="w-100 h-100 m-0 p-0 overflow-hidden">
            <div class="d-flex flex-row gap-4" style="transition: transform 0.3s ease;" :style="{ transform: 'translateX(-' + (currentIndexFourthSection * 100) / blocksVisibleFourthSection + '%)' }">
              <button class="btn py-1 px-3 border-light border-1" style="text-wrap: nowrap;" v-for="(block, index) in blocksFourthSection" :key="index">{{ block }}</button>
            </div>
          </div>
          <!-- Tombol Next -->
          <button class="next btn border-light border-1 px-4 py-1 m-0 d-flex flex-row align-items-center gap-2" :disabled="currentIndexFourthSection >= blocksFourthSection.length - blocksVisibleFourthSection" style="transition: background-color 0.3s ease; cursor: pointer;" @click="moveSliderFourthSection('next')">
            Next
            <i class="bi bi-caret-right"></i>
          </button>
        </div>
      </section>
    </div>
  </div>
</template>
<style>
@media (max-width: 1200px) {
  #app {
    display: none !important;
  }
  #justWarnning {
    display: block !important;
  }
}
</style>
<style scoped>
button:disabled {
  background-color: #888;
  cursor: not-allowed;
}
</style>
<script>
import columnCountModalComponent from '@/components/columnCountModalComponent.vue';

export default {
  components: {
    columnCountModalComponent
  },
  data() {
    return {
      url: '',
      logs_url: [],
      currentPrevUrls: [],
      // Second Section Data
      currentIndexSecondSection: 0,
      blocksSecondSection: [
        {
          name: 'Column Count',
          column_modal_id: '#columnCountModal'
        },
        {
          name: 'Union Statements',
          column_modal_id: ''
        },
        {
          name: 'Basic Statements',
          column_modal_id: ''
        },
        {
          name: 'DIOS',
          column_modal_id: ''
        },
        {
          name: 'Local Variable',
          column_modal_id: ''
        },
        {
          name: 'Error Based',
          column_modal_id: ''
        },
        {
          name: 'Print System',
          column_modal_id: ''
        },
        {
          name: 'Double Query',
          column_modal_id: ''
        },
        {
          name: 'XPath Injection',
          column_modal_id: ''
        },
        {
          name: 'MSSQL',
          column_modal_id: ''
        },
        {
          name: 'PostgreSQL',
          column_modal_id: ''
        },
        {
          name: 'LFI',
          column_modal_id: ''
        },
        {
          name: 'RCE',
          column_modal_id: ''
        },
        {
          name: 'XSS',
          column_modal_id: ''
        },
        {
          name: 'Custom Query',
          column_modal_id: ''
        }
      ],
      blocksVisibleSecondSection: 6,
      // Third Section Data
      currentIndexThirdSection: 0,
      blocksThirdSection: [
        'Replace',
        'WAF Bypass',
        'URL Balancer',
        'Polygon',
        'Writeable Path',
        'Auth Bypass',
        'User Privileges',
        'Uploader',
        'Extract Links',
      ],
      blocksVisibleThirdSection: 5,
      // Fourth Section Data
      currentIndexFourthSection: 0,
      blocksFourthSection: [
        'Find',
        'View Source',
        'Post Data: off',
        'Tamper Data: off',
        'Javascript: on',
        'No Redirect: off',
        'Admin Finder',
        'Admin Scanner',
        'Web Tools',
        'User Agent'
      ],
      blocksVisibleFourthSection: 5,
    }
  },
  watch: {
    url(newUrl, oldUrl) {
      if (newUrl !== oldUrl && newUrl !== '') {
        if (this.logs_url[this.logs_url.length - 1] !== newUrl) {
          this.logs_url.push(newUrl);
        }
      }
    }
  },
  methods: {
    clearUrlData() {
      this.url = "";
      this.logs_url = [];
      this.currentPrevUrls = [];
    },
    prevUrls() {
      // Reset currentPrevUrls jika URL baru diketik
      if (this.url !== this.logs_url[this.logs_url.length - 1]) {
        this.currentPrevUrls = [];
      }

      if (this.logs_url.length >= 1) {
        this.logs_url.pop();
        this.currentPrevUrls.push(this.url);
        this.url = this.logs_url[this.logs_url.length - 1];
      } else {
        alert("No previous URL found");
      }
    },
    nextUrls() {
      if (this.currentPrevUrls.length > 0) {
        // Ambil URL berikutnya dari currentPrevUrls
        const nextUrl = this.currentPrevUrls.pop();
        this.logs_url.push(this.url);
        this.url = nextUrl;
      } else {
        alert("No next URL found");
      }
    },
    moveSliderSecondSection(direction) {
      const totalBlocks = this.blocksSecondSection.length;
      if (direction === 'next') {
        if (this.currentIndexSecondSection < totalBlocks - this.blocksVisibleSecondSection) {
          this.currentIndexSecondSection++;
        }
      } else if (direction === 'prev') {
        if (this.currentIndexSecondSection > 0) {
          this.currentIndexSecondSection--;
        }
      }
    },
    moveSliderThirdSection(direction) {
      const totalBlocks = this.blocksThirdSection.length;
      if (direction === 'next') {
        if (this.currentIndexThirdSection < totalBlocks - this.blocksVisibleThirdSection) {
          this.currentIndexThirdSection++;
        }
      } else if (direction === 'prev') {
        if (this.currentIndexThirdSection > 0) {
          this.currentIndexThirdSection--;
        }
      }
    },
    moveSliderFourthSection(direction) {
      const totalBlocks = this.blocksFourthSection.length;
      if (direction === 'next') {
        if (this.currentIndexFourthSection < totalBlocks - this.blocksVisibleFourthSection) {
          this.currentIndexFourthSection++;
        }
      } else if (direction === 'prev') {
        if (this.currentIndexFourthSection > 0) {
          this.currentIndexFourthSection--;
        }
      }
    },
    insertAtCursor(text) {
      const textarea = this.$refs.textarea;
      
      if (!this.url) {
        // Jika this.url kosong, set ke string kosong
        this.url = '';
      }

      const cursorStart = textarea.selectionStart;
      const cursorEnd = textarea.selectionEnd;

      this.url =
        this.url.substring(0, cursorStart) +
        text +
        this.url.substring(cursorEnd);

      this.$nextTick(() => {
        textarea.setSelectionRange(cursorStart + text.length, cursorStart + text.length);
        textarea.focus();
      });
    },
    updateUrlData(payload) {
      this.insertAtCursor(payload)
    }
  }
}
</script>
