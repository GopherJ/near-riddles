<template>
  <div>
    <h3>Answer Riddle</h3>
    <br />

    <b-table
      :data="data"
      :bordered="isBordered"
      :striped="isStriped"
      :narrowed="isNarrowed"
      :hoverable="isHoverable"
      :loading="isLoading"
      :focusable="isFocusable"
    >
      <b-table-column field="id" label="ID" width="40" numeric v-slot="props">
        {{ props.row.id }}
      </b-table-column>
    </b-table>

    <b-field label="answer">
      <b-input v-model="answer" placeholder="enter the answer"></b-input>
    </b-field>

    <br />

    <b-field>
      <b-button @click="answer_riddle">Submit</b-button>
    </b-field>
  </div>
</template>

<script>
import sha256 from 'js-sha256'

export default {
  name: 'AnswerRiddle',
  data() {
    return {
      isEmpty: false,
      isBordered: false,
      isStriped: false,
      isNarrowed: false,
      isHoverable: false,
      isFocusable: false,
      isLoading: false,
      selectedQuestionId: null,
      questionList: [],
      answer: null,
      data: [
        {
          id: 1,
          first_name: 'Jesse',
          last_name: 'Simmons',
          date: '2016-10-15 13:43:27',
          gender: 'Male',
        },
      ],
    }
  },
  methods: {
    answer_riddle: async function() {
      if (!this.selectedQuestionId) {
        window.alert("You haven't selected any question")
        return
      }

      if (!this.answer) {
        window.alert("You haven't filled the form'")
        return
      }

      try {
        await window.contract.answer_riddle({
          id: this.selectedQuestionId,
          sha256_answer: sha256(this.answer),
        })
      } catch (e) {
        window.alert(
          'Something went wrong! ' +
            'Maybe you need to sign out and back in? ' +
            'Check your browser console for more info.'
        )
      }
    },
  },
}
</script>

<style type="text/css"></style>
