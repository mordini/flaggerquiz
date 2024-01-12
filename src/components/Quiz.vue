<script setup lang="ts">
import 'survey-core/defaultV2.min.css';
import { Model } from 'survey-core';
import { onBeforeMount } from 'vue';

// SET UP THE SURVEY
const surveyJson = {
  title: 'Flagging Knowledge',
  showProgressBar: 'bottom',
  showTimerPanel: 'top',
  maxTimeToFinishPage: 0,
  maxTimeToFinish: 0,
  firstPageIsStarted: true,
  questionsOrder: 'random',

  // NOT A NATIVE PROPERTY, ADDED ENHANCEMENT FOR RANDOMIZING PAGE ORDER
  pageOrderRandom: true,
  startSurveyText: 'Start Quiz',
  pages: [
    {
      elements: [
        {
          type: 'html',
          html: 'You are about to start a quiz on Flagging. <br>You will have 10 seconds for every question and 25 seconds to end the quiz.<br>Enter your name below and click <b>Start Quiz</b> to begin.',
        },
        {
          type: 'text',
          name: 'username',
          titleLocation: 'hidden',
          isRequired: true,
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'flaggingtaper',
          title: 'How many cones in a flagging taper?',
          choicesOrder: 'random',
          choices: ['3', '12', '6', '82'],
          correctAnswer: '6',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'conesbuffer35mph',
          title: 'How many cones in a buffer space for 35MPH?',
          choicesOrder: 'random',
          choices: ['82', '16', '10', '35'],
          correctAnswer: '10',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'conesbuffer35mphsteps',
          title:
            'How many steps apart do the cones need to be in a buffer space for 35MPH?',
          choicesOrder: 'random',
          choices: ['82', '16', '10', '35'],
          correctAnswer: '10',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'conesbuffer45mph',
          title: 'How many cones in a buffer space for 45MPH?',
          choicesOrder: 'random',
          choices: ['82', '9', '10', '35'],
          correctAnswer: '9',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'conesbuffer45mphsteps',
          title:
            'How many steps apart do the cones need to be in a buffer space for 45MPH?',
          choicesOrder: 'random',
          choices: ['82', '16', '10', '20'],
          correctAnswer: '20',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'conesbuffer55mph',
          title: 'How many cones in a buffer space for 55MPH?',
          choicesOrder: 'random',
          choices: ['82', '9', '10', '12'],
          correctAnswer: '12',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'conesbuffer55mphsteps',
          title:
            'How many steps apart do the cones need to be in a buffer space for 55MPH?',
          choicesOrder: 'random',
          choices: ['82', '16', '10', '20'],
          correctAnswer: '20',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'signspacing35mph',
          title: 'What is the spacing in feet between signs at 35MPH?',
          choicesOrder: 'random',
          choices: ['1,000', '500', '350', '200'],
          correctAnswer: '200',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'signspacing45mph',
          title: 'What is the spacing in feet between signs at 45MPH?',
          choicesOrder: 'random',
          choices: ['1,000', '500', '350', '200'],
          correctAnswer: '350',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'signspacing55mph',
          title: 'What is the spacing in feet between signs at 55MPH?',
          choicesOrder: 'random',
          choices: ['1,000', '500', '350', '200'],
          correctAnswer: '500',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'signspacingruralcountry',
          title:
            'What is the spacing in feet between signs on rural (country) roads?',
          choicesOrder: 'random',
          choices: ['1,000', '500', '350', '200'],
          correctAnswer: '500',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'flaggingsignone',
          title: 'What is the first sign in a flagging package?',
          choicesOrder: 'random',
          choices: [
            'Be Prepared To Stop',
            'One Lane Road Ahead',
            'Flagging Symbol',
            'Lane Shift Ahead',
          ],
          correctAnswer: 'One Lane Road Ahead',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'flaggingsigntwo',
          title: 'What is the second sign in a flagging package?',
          choicesOrder: 'random',
          choices: [
            'Be Prepared To Stop',
            'Road Work Ahead',
            'Flagging Symbol',
            'Lane Shift Ahead',
          ],
          correctAnswer: 'Be Prepared To Stop',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'flaggingsignthree',
          title: 'What is the third sign in a flagging package?',
          choicesOrder: 'random',
          choices: [
            'Be Prepared To Stop',
            'Road Work Ahead',
            'Flagging Symbol',
            'Lane Shift Ahead',
          ],
          correctAnswer: 'Flagging Symbol',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'roadclosedfirstsign',
          title: 'What is the first sign for a Road Closed package?',
          choicesOrder: 'random',
          choices: [
            'Road Closed',
            'Road Closed Ahead',
            'Flagging Symbol',
            'Road Work Ahead',
          ],
          correctAnswer: 'Road Work Ahead',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'roadclosedsecondsign',
          title: 'What is the second sign for a Road Closed package?',
          choicesOrder: 'random',
          choices: [
            'Road Closed',
            'Road Closed Ahead',
            'Flagging Symbol',
            'Road Work Ahead',
          ],
          correctAnswer: 'Road Closed Ahead',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'roadclosedthirdsign',
          title: 'What is the third sign for a Road Closed package?',
          choicesOrder: 'random',
          choices: [
            'Road Closed',
            'Road Closed Ahead',
            'Flagging Symbol',
            'Road Work Ahead',
          ],
          correctAnswer: 'Road Closed',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'cones35mph',
          title: 'How many cones go in the middle of the road in a 35MPH zone?',
          choicesOrder: 'random',
          choices: ['11', '15', '35', '7'],
          correctAnswer: '7',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'cones45mph',
          title: 'How many cones go in the middle of the road in a 45MPH zone?',
          choicesOrder: 'random',
          choices: ['11', '15', '35', '14'],
          correctAnswer: '14',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'cones55mph',
          title: 'How many cones go in the middle of the road in a 55MPH zone?',
          choicesOrder: 'random',
          choices: ['11', '17', '55', '7'],
          correctAnswer: '17',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'arrowboardfirstsign',
          title: "What's the first sign in a Arrow Board package?",
          choicesOrder: 'random',
          choices: [
            'Arrow Board',
            'Right Lane Closed Ahead',
            'Merge Symbol',
            'Right Lane Closed',
          ],
          correctAnswer: 'Right Lane Closed Ahead',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'arrowboardsecondsign',
          title: "What's the second sign in a Arrow Board package?",
          choicesOrder: 'random',
          choices: [
            'Arrow Board',
            'Right Lane Closed Ahead',
            'Merge Symbol',
            'Right Lane Closed',
          ],
          correctAnswer: 'Merge Symbol',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'arrowboardthirdsign',
          title: "What's the third sign in a Arrow Board package?",
          choicesOrder: 'random',
          choices: [
            'Arrow Board',
            'Right Lane Closed Ahead',
            'Merge Symbol',
            'Right Lane Closed',
          ],
          correctAnswer: 'Right Lane Closed',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'shoulderfirstsign',
          title: "What's the first sign in a Shoulder package?",
          choicesOrder: 'random',
          choices: [
            'Road Work Ahead',
            'Shoulder Closed Ahead',
            'Shoulder Closed',
            'One Lane Road Ahead',
          ],
          correctAnswer: 'Road Work Ahead',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'shouldersecondsign',
          title: "What's the second sign in a Shoulder package?",
          choicesOrder: 'random',
          choices: [
            'Road Work Ahead',
            'Shoulder Closed Ahead',
            'Shoulder Closed',
            'One Lane Road Ahead',
          ],
          correctAnswer: 'Shoulder Closed Ahead',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'shoulderthirdsign',
          title: "What's the third sign in a Shoulder package?",
          choicesOrder: 'random',
          choices: [
            'Road Work Ahead',
            'Shoulder Close Ahead',
            'Shoulder Closed',
            'One Lane Road Ahead',
          ],
          correctAnswer: 'Shoulder Closed',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'fivepackages',
          title: 'What are the five packages?',
          choicesOrder: 'random',
          choices: [
            'Flagging, Road Closed, Shoulder, Lane Shift, Arrow Board',
            'Flagging, Road Closed, Right Lane Closed, Lane Shift, Arrow Board',
            'Flagging, Road Closed, Shoulder, Lane Shift, Be Prepared To Stop',
            'Flagging, One Lane Road Ahead, Shoulder, Lane Shift, Arrow Board',
          ],
          correctAnswer:
            'Flagging, Road Closed, Shoulder, Lane Shift, Arrow Board',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'laneshiftsignone',
          title: "What's the first sign in a Lane Shift package?",
          choicesOrder: 'random',
          choices: [
            'Road Work Ahead',
            'Lane Shift Symbol',
            'One Lane Road Ahead',
            'Lane Shift Ahead',
          ],
          correctAnswer: 'Road Work Ahead',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'laneshiftsigntwo',
          title: "What's the second sign in a Lane Shift package?",
          choicesOrder: 'random',
          choices: [
            'Road Work Ahead',
            'Lane Shift Symbol',
            'One Lane Road Ahead',
            'Lane Shift Ahead',
          ],
          correctAnswer: 'Lane Shift Ahead',
        },
      ],
    },
    {
      elements: [
        {
          type: 'radiogroup',
          name: 'laneshiftsignthree',
          title: "What's the third sign in a Lane Shift package?",
          choicesOrder: 'random',
          choices: [
            'Road Work Ahead',
            'Lane Shift Symbol',
            'One Lane Road Ahead',
            'Lane Shift Ahead',
          ],
          correctAnswer: 'Lane Shift Symbol',
        },
      ],
    },
  ],
  completedHtml:
    '<h4>You got <b>{correctAnswers}</b> out of <b>{questionCount}</b> correct answers.</h4>',
  completedHtmlOnCondition: [
    {
      expression: '{correctAnswers} == 0',
      html: '<h4>Unfortunately, none of your answers are correct. Please try again.</h4>',
    },
    {
      expression: '{correctAnswers} == {questionCount}',
      html: '<h4>Congratulations! You answered all the questions correctly!</h4>',
    },
  ],
};

// FUNCTION TO RANDOMIZE ARRAY
const shuffleArray = (arr) =>
  arr
    .map((a) => [Math.random(), a])
    .sort((a, b) => a[0] - b[0])
    .map((a) => a[1]);

// FUNCTION TO SHUFFLE THE PAGES IF THE PROPERTY IS SET
function shufflePages() {
  console.warn(`SHUFFLING PAGES`);
  // GET THE FIRST PAGE FOR REINSERTION
  const firstPage = surveyJson.pages[0];
  // REMOVE FIRST PAGE
  surveyJson.pages.shift();
  // RANDOMIZE surveyJson.pages
  surveyJson.pages = shuffleArray(surveyJson.pages);
  // REINSERT THE FIRST PAGE
  surveyJson.pages.unshift(firstPage);
}

// CHECK TO SEE IF WE NEED TO SHUFFLE PAGES AND DO SO IF NEEDED
// THIS IS OUTSIDE OF A LIFECYCLE HOOK TO RUN BEFORE CREATING survey model
if (surveyJson.pageOrderRandom) shufflePages();

// MAKE THAT SURVEY
const survey = new Model(surveyJson);
</script>

<template>
  <SurveyComponent :model="survey" />
</template>
