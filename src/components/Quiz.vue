<script setup lang="ts">
import 'survey-core/defaultV2.min.css';
import { Model } from 'survey-core';
import { onBeforeMount } from 'vue';
import axios from 'axios';

// SET UP THE SURVEY
const quizJson = {
  title: 'Flagging Quiz',
  showProgressBar: 'bottom',
  showTimerPanel: 'top',
  maxTimeToFinishPage: 0,
  maxTimeToFinish: 0,
  firstPageIsStarted: true,
  questionsOrder: 'random',

  // NOT A NATIVE PROPERTY, ADDED ENHANCEMENT FOR RANDOMIZING PAGE ORDER
  randomPageOrder: true,

  startSurveyText: 'Start Quiz',
  pages: [
    {
      elements: [
        {
          type: 'html',
          html: 'You are about to start a quiz on Flagging. <br/><br/>Enter your name and click <b>Start Quiz</b> to begin. <br/><br/> NOTE:  If you started this quiz before and did not finish, your previous answers will be restored, but the questions may be in a different order.',
        },
        {
          type: 'text',
          name: 'firstName',
          title: 'First Name',
          isRequired: true,
        },
        {
          type: 'text',
          name: 'lastName',
          title: 'Last Name',
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
          isRequired: true,
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
          isRequired: true,
        },
      ],
    },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'conesbuffer35mphsteps',
    //       title:
    //         'How many steps apart do the cones need to be in a buffer space for 35MPH?',
    //       choicesOrder: 'random',
    //       choices: ['82', '16', '10', '35'],
    //       correctAnswer: '10',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'conesbuffer45mph',
    //       title: 'How many cones in a buffer space for 45MPH?',
    //       choicesOrder: 'random',
    //       choices: ['82', '9', '10', '35'],
    //       correctAnswer: '9',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'conesbuffer45mphsteps',
    //       title:
    //         'How many steps apart do the cones need to be in a buffer space for 45MPH?',
    //       choicesOrder: 'random',
    //       choices: ['82', '16', '10', '20'],
    //       correctAnswer: '20',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'conesbuffer55mph',
    //       title: 'How many cones in a buffer space for 55MPH?',
    //       choicesOrder: 'random',
    //       choices: ['82', '9', '10', '12'],
    //       correctAnswer: '12',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'conesbuffer55mphsteps',
    //       title:
    //         'How many steps apart do the cones need to be in a buffer space for 55MPH?',
    //       choicesOrder: 'random',
    //       choices: ['82', '16', '10', '20'],
    //       correctAnswer: '20',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'signspacing35mph',
    //       title: 'What is the spacing in feet between signs at 35MPH?',
    //       choicesOrder: 'random',
    //       choices: ['1,000', '500', '350', '200'],
    //       correctAnswer: '200',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'signspacing45mph',
    //       title: 'What is the spacing in feet between signs at 45MPH?',
    //       choicesOrder: 'random',
    //       choices: ['1,000', '500', '350', '200'],
    //       correctAnswer: '350',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'signspacing55mph',
    //       title: 'What is the spacing in feet between signs at 55MPH?',
    //       choicesOrder: 'random',
    //       choices: ['1,000', '500', '350', '200'],
    //       correctAnswer: '500',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'signspacingruralcountry',
    //       title:
    //         'What is the spacing in feet between signs on rural (country) roads?',
    //       choicesOrder: 'random',
    //       choices: ['1,000', '500', '350', '200'],
    //       correctAnswer: '500',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'flaggingsignone',
    //       title: 'What is the first sign in a flagging package?',
    //       choicesOrder: 'random',
    //       choices: [
    //         'Be Prepared To Stop',
    //         'One Lane Road Ahead',
    //         'Flagging Symbol',
    //         'Lane Shift Ahead',
    //       ],
    //       correctAnswer: 'One Lane Road Ahead',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'flaggingsigntwo',
    //       title: 'What is the second sign in a flagging package?',
    //       choicesOrder: 'random',
    //       choices: [
    //         'Be Prepared To Stop',
    //         'Road Work Ahead',
    //         'Flagging Symbol',
    //         'Lane Shift Ahead',
    //       ],
    //       correctAnswer: 'Be Prepared To Stop',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'flaggingsignthree',
    //       title: 'What is the third sign in a flagging package?',
    //       choicesOrder: 'random',
    //       choices: [
    //         'Be Prepared To Stop',
    //         'Road Work Ahead',
    //         'Flagging Symbol',
    //         'Lane Shift Ahead',
    //       ],
    //       correctAnswer: 'Flagging Symbol',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'roadclosedfirstsign',
    //       title: 'What is the first sign for a Road Closed package?',
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Closed',
    //         'Road Closed Ahead',
    //         'Flagging Symbol',
    //         'Road Work Ahead',
    //       ],
    //       correctAnswer: 'Road Work Ahead',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'roadclosedsecondsign',
    //       title: 'What is the second sign for a Road Closed package?',
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Closed',
    //         'Road Closed Ahead',
    //         'Flagging Symbol',
    //         'Road Work Ahead',
    //       ],
    //       correctAnswer: 'Road Closed Ahead',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'roadclosedthirdsign',
    //       title: 'What is the third sign for a Road Closed package?',
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Closed',
    //         'Road Closed Ahead',
    //         'Flagging Symbol',
    //         'Road Work Ahead',
    //       ],
    //       correctAnswer: 'Road Closed',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'cones35mph',
    //       title: 'How many cones go in the middle of the road in a 35MPH zone?',
    //       choicesOrder: 'random',
    //       choices: ['11', '15', '35', '7'],
    //       correctAnswer: '7',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'cones45mph',
    //       title: 'How many cones go in the middle of the road in a 45MPH zone?',
    //       choicesOrder: 'random',
    //       choices: ['11', '15', '35', '14'],
    //       correctAnswer: '14',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'cones55mph',
    //       title: 'How many cones go in the middle of the road in a 55MPH zone?',
    //       choicesOrder: 'random',
    //       choices: ['11', '17', '55', '7'],
    //       correctAnswer: '17',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'arrowboardfirstsign',
    //       title: "What's the first sign in a Arrow Board package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Arrow Board',
    //         'Right Lane Closed Ahead',
    //         'Merge Symbol',
    //         'Right Lane Closed',
    //       ],
    //       correctAnswer: 'Right Lane Closed Ahead',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'arrowboardsecondsign',
    //       title: "What's the second sign in a Arrow Board package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Arrow Board',
    //         'Right Lane Closed Ahead',
    //         'Merge Symbol',
    //         'Right Lane Closed',
    //       ],
    //       correctAnswer: 'Merge Symbol',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'arrowboardthirdsign',
    //       title: "What's the third sign in a Arrow Board package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Arrow Board',
    //         'Right Lane Closed Ahead',
    //         'Merge Symbol',
    //         'Right Lane Closed',
    //       ],
    //       correctAnswer: 'Right Lane Closed',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'shoulderfirstsign',
    //       title: "What's the first sign in a Shoulder package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Work Ahead',
    //         'Shoulder Closed Ahead',
    //         'Shoulder Closed',
    //         'One Lane Road Ahead',
    //       ],
    //       correctAnswer: 'Road Work Ahead',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'shouldersecondsign',
    //       title: "What's the second sign in a Shoulder package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Work Ahead',
    //         'Shoulder Closed Ahead',
    //         'Shoulder Closed',
    //         'One Lane Road Ahead',
    //       ],
    //       correctAnswer: 'Shoulder Closed Ahead',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'shoulderthirdsign',
    //       title: "What's the third sign in a Shoulder package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Work Ahead',
    //         'Shoulder Close Ahead',
    //         'Shoulder Closed',
    //         'One Lane Road Ahead',
    //       ],
    //       correctAnswer: 'Shoulder Closed',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'fivepackages',
    //       title: 'What are the five packages?',
    //       choicesOrder: 'random',
    //       choices: [
    //         'Flagging, Road Closed, Shoulder, Lane Shift, Arrow Board',
    //         'Flagging, Road Closed, Right Lane Closed, Lane Shift, Arrow Board',
    //         'Flagging, Road Closed, Shoulder, Lane Shift, Be Prepared To Stop',
    //         'Flagging, One Lane Road Ahead, Shoulder, Lane Shift, Arrow Board',
    //       ],
    //       correctAnswer:
    //         'Flagging, Road Closed, Shoulder, Lane Shift, Arrow Board',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'laneshiftsignone',
    //       title: "What's the first sign in a Lane Shift package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Work Ahead',
    //         'Lane Shift Symbol',
    //         'One Lane Road Ahead',
    //         'Lane Shift Ahead',
    //       ],
    //       correctAnswer: 'Road Work Ahead',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'laneshiftsigntwo',
    //       title: "What's the second sign in a Lane Shift package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Work Ahead',
    //         'Lane Shift Symbol',
    //         'One Lane Road Ahead',
    //         'Lane Shift Ahead',
    //       ],
    //       correctAnswer: 'Lane Shift Ahead',
    //       isRequired: true,
    //     },
    //   ],
    // },
    // {
    //   elements: [
    //     {
    //       type: 'radiogroup',
    //       name: 'laneshiftsignthree',
    //       title: "What's the third sign in a Lane Shift package?",
    //       choicesOrder: 'random',
    //       choices: [
    //         'Road Work Ahead',
    //         'Lane Shift Symbol',
    //         'One Lane Road Ahead',
    //         'Lane Shift Ahead',
    //       ],
    //       correctAnswer: 'Lane Shift Symbol',
    //       isRequired: true,
    //     },
    //   ],
    // },
  ],
  completedHtml:
    '<h4>You got <b>{correctAnswers}</b> out of <b>{questionCount}</b> correct answers.</h4><br/><br/><button onclick="location.reload()">Go To Beginning</button>',
  completedHtmlOnCondition: [
    {
      expression: '{correctAnswers} == 0',
      html: '<h4>Unfortunately, none of your answers are correct. Please try again.</h4><br/><br/><button onclick="location.reload()">Go To Beginning</button>',
    },
    {
      expression: '{correctAnswers} == {questionCount}',
      html: '<h4>Congratulations! You answered all the questions correctly!</h4><br/><br/><button onclick="location.reload()">Go To Beginning</button>',
    },
  ],
};

// FUNCTION TO RANDOMIZE ARRAY
const shuffleArray = (arr: any) =>
  arr
    .map((a: any) => [Math.random(), a])
    .sort((a: any, b: any) => a[0] - b[0])
    .map((a: any) => a[1]);

// FUNCTION TO SHUFFLE THE PAGES IF THE PROPERTY IS SET
function shufflePages() {
  console.warn(`SHUFFLING PAGES`);

  // GET THE FIRST PAGE FOR REINSERTION
  const firstPage = quizJson.pages[0];

  // REMOVE FIRST PAGE
  quizJson.pages.shift();

  // RANDOMIZE quizJson.pages
  quizJson.pages = shuffleArray(quizJson.pages);

  // REINSERT THE FIRST PAGE
  quizJson.pages.unshift(firstPage);
}

// CHECK TO SEE IF WE NEED TO SHUFFLE PAGES AND DO SO IF NEEDED
// THIS IS OUTSIDE OF A LIFECYCLE HOOK TO RUN BEFORE CREATING survey model
if (quizJson.randomPageOrder) shufflePages();

// MAKE THAT SURVEY NOW THAT WE HANDLED SHUFFLING OR NOT
const survey = new Model(quizJson);

/**********************/
/* SESSION MANAGEMENT */
/**********************/

// KEY FOR LOCAL STORAGE
const storageItemKey = 'flagger-survey';

// FUNCTION TO SAVE THE SURVEY DATA
function saveSurveyData(survey: any) {
  // HOLD THE DATA
  const data = survey.data;

  // SET THE CURRENT PAGE NUMBER
  data.pageNo = survey.currentPageNo;

  // PUT IN LOCALSTORAGE
  window.localStorage.setItem(storageItemKey, JSON.stringify(data));
}

// SAVE SURVEY RESULTS TO LOCAL STORAGE WHEN WE CHANGE THINGS
survey.onValueChanged.add(saveSurveyData);
survey.onCurrentPageChanged.add(saveSurveyData);

// GET RID OF THE RESET BUTTON AFTER QUIZ STARTS
survey.onStarted.add(() => {
  // WAIT FOR THE PAGE TO RENDER BEFORE HIDING
  survey.onAfterRenderPage.add(() => {
    hideResetButton(true);
  });
});

// RESTORE SURVEY RESULTS
const prevData = window.localStorage.getItem(storageItemKey) || null;

// IF THERE IS PREVIOUS DATA
if (prevData) {
  // GET THE PREVIOUS DATA
  const data = JSON.parse(prevData);

  // PUT THE DATA BACK
  survey.data = data;

  // IF THERE IS PREVIOUS DATA
  if (data.pageNo && !quizJson.randomPageOrder) {
    // NAVIGATE TO THE LAST PAGE (NOT GREAT)
    survey.currentPageNo = data.pageNo;
  }
}

// FUNCTION TO HIDE OR SHOW THE RESET BUTTON
function hideResetButton(doHide: boolean) {
  // GET THE RESET BUTTON
  const resetButton = document.querySelectorAll(
    '#sv-nav-reset-quiz'
  ) as NodeListOf<HTMLDivElement>;

  // CHECK IF WE NEED TO HIDE OR NOT
  if (doHide) {
    console.warn(`HIDE RESET BUTTON`);
    resetButton[0].classList.add('hideElement');
  } else {
    console.warn(`SHOW RESET BUTTON`);
    resetButton[0].classList.remove('hideElement');
  }
}

// FUNCTION TO RESET QUIZ
function resetQuiz() {
  console.warn(`RESETTING QUIZ`);
  survey.clear();
  window.localStorage.removeItem(storageItemKey);
}

survey.addNavigationItem({
  id: 'sv-nav-reset-quiz',
  title: 'Clear Previous Answers',

  // CLEAR THE LOCAL STORAGE OF QUIZ STUFF
  action: () => {
    resetQuiz();
    // window.localStorage.removeItem(storageItemKey);
    // window.localStorage.setItem(storageItemKey, '');
  },
  css: 'nav-button',
  innerCss: 'sd-btn nav-input',
});

// FUNCTION TO POST RESULTS
function postToApi(quizResults) {
  // console.log(quizResults);
  console.log(`SENDING RESULT`);
  // console.log(quizResults);
  axios
    .post('http://paulmordini.com:5000/results', quizResults)
    .then((res) => {
      console.log(res);
    })
    .catch((error) => {
      console.log(error);
    });
}
survey.onComplete.add((sender, options) => {
  // DISPLAY MESSAGE OF SAVING
  options.showSaveInProgress();

  // POST THE DATA TO THE API
  postToApi(sender.data);
});

// EMPTY LOCAL STORAGE AFTER FINISHING SURVEY
// survey.onComplete.add(() => window.localStorage.setItem(storageItemKey, ''));
// survey.onComplete.add(() => resetQuiz());
// survey.onComplete.add(() => hideResetButton(false));

// RESTORE SESSION FOR PERSON WITH NAME MAYBE
// DO THIS LATER
</script>

<template>
  <SurveyComponent :model="survey" />
</template>

<style>
.hideElement {
  display: none;
}
</style>
