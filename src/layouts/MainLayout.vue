<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>


        <q-toolbar-title style="padding-left: 10px">
          Генератор
        </q-toolbar-title>

        <div>Карточка студента</div>
      </q-toolbar>
    </q-header>



    <q-page-container>
      <div v-for="student in students" :key="student">
        <fieldset style="margin: 20px">
          <q-input v-model="student.fio" label="ФИО" />
          <q-input v-model="student.birth_date" label="Дата рождения" />
          <q-input v-model="student.education" label="Образование" />
          <q-input v-model="student.telephone" label="Номер телефона" />
          <q-input v-model="student.address" label="Место жительства" />
          <q-input v-model="student.fuc" label="Факультет" />
          <q-input v-model="student.course" label="Курс" />
        </fieldset>
        <br>
      </div>

      <div style="padding-left: 20px">
      <q-btn icon="add" @click="students.push(Object.create(student))"/>
      <q-btn @click="generate">Сгенерировать</q-btn>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import * as fs from "fs";
import { AlignmentType, Document, HeadingLevel, Packer, Paragraph, TabStopPosition, TabStopType, TextRun } from "docx";
import * as docx from "docx";



export default defineComponent({
  name: 'MainLayout',

  components: {

  },

  data() {
    return {
      students: [
          {
            fio: '',
            birth_date: '',
            education: '',
            telephone: '',
            address: '',
            fuc: '',
            course: '',
          }
      ],
      student: {
        fio: '',
        birth_date: '',
        education: '',
        telephone: '',
        address: '',
        fuc: '',
        course: '',
      }
    }
  },
  methods: {
    // test(){
    //   let doc = new docx.Document();
    //   for(let i = 0; i < this.students.length; i++) {
    //
    //
    //
    //     doc.addSection({
    //       children: [
    //         new docx.Paragraph({
    //           children: [
    //             new docx.TextRun({
    //               text: 'Карточка студента',
    //               heading: HeadingLevel.HEADING_1,
    //               alignment: AlignmentType.CENTER,
    //               bold: true,
    //             })
    //           ]
    //         }),
    //         new docx.Paragraph({
    //           children: [
    //             new docx.TextRun({
    //               text: `ФИО: ${this.students[i].fio}`
    //             })
    //           ]
    //         }),
    //         new docx.Paragraph({
    //           children: [
    //             new docx.TextRun({
    //               text: `Дата рождения: ${this.students[i].birth_date}`
    //             })
    //           ]
    //         }),
    //         new docx.Paragraph({
    //           children: [
    //             new docx.TextRun({
    //               text: `Образование: ${this.students[i].education}`
    //             })
    //           ]
    //         }),
    //         new docx.Paragraph({
    //           children: [
    //             new docx.TextRun({
    //               text: `Номер телефона: ${this.students[i].telephone}`
    //             })
    //           ]
    //         }),
    //         new docx.Paragraph({
    //           children: [
    //             new docx.TextRun({
    //               text: `Место жительства: ${this.students[i].address}`
    //             })
    //           ]
    //         }),
    //         new docx.Paragraph({
    //           children: [
    //             new docx.TextRun({
    //               text: `Факультет: ${this.students[i].fuc}`
    //             })
    //           ]
    //         }),
    //         new docx.Paragraph({
    //           children: [
    //             new docx.TextRun({
    //               text: `Курс: ${this.students[i].course}`
    //             })
    //           ]
    //         })
    //       ]
    //     })
    //   }
    //   docx.Packer.toBlob(doc).then((blob) => {
    //     saveAs(blob, 'hi.docx')
    //   });
    // },
    generate() {

      let doc = new Document({ sections: [] })
      for(let i = 0; i < this.students.length; i++) {


        doc.addSection({
          children: [
            // new Paragraph({text: `ФИО ${this.students[i].fio}`, heading: HeadingLevel.TITLE}),
            new Paragraph({text: `Карточка студента \n`, heading: HeadingLevel.HEADING_1, alignment: AlignmentType.CENTER}),
            new Paragraph({text: ''}),
            new Paragraph({text: `ФИО: ${this.students[i].fio}`, heading: HeadingLevel.HEADING_3}),
            new Paragraph({text: `Место жительства ${this.students[i].address}`, heading: HeadingLevel.HEADING_3}),
            new Paragraph({text: `Телефон ${this.students[i].telephone}`, heading: HeadingLevel.HEADING_3}),
            new Paragraph({text: `Дата рождения ${this.students[i].birth_date}`, heading: HeadingLevel.HEADING_3}),
            new Paragraph({text: `Образование ${this.students[i].education}`, heading: HeadingLevel.HEADING_3}),
            new Paragraph({text: `Факультет ${this.students[i].fuc}`, heading: HeadingLevel.HEADING_3}),
            new Paragraph({text: `Курс ${this.students[i].course}`, heading: HeadingLevel.HEADING_3}),
            // new Paragraph({
            //   text:
            //     "Aliquam gravida quam sapien, quis dapibus eros malesuada vel. Praesent tempor aliquam iaculis. Nam ut neque ex. Curabitur pretium laoreet nunc, ut ornare augue aliquet sed. Pellentesque laoreet sem risus. Cras sodales libero convallis, convallis ex sed, ultrices neque. Sed quis ullamcorper mi. Ut a leo consectetur, scelerisque nibh sit amet, egestas mauris. Donec augue sapien, vestibulum in urna et, cursus feugiat enim. Ut sit amet placerat quam, id tincidunt nulla. Cras et lorem nibh. Suspendisse posuere orci nec ligula mattis vestibulum. Suspendisse in vestibulum urna, non imperdiet enim. Vestibulum vel dolor eget neque iaculis ultrices."
            // })
          ]
        });
      }

        // console.log(doc)
        Packer.toBlob(doc).then((blob) => {
          saveAs(blob, 'hi.docx')
        });
    }
  }
})
</script>
