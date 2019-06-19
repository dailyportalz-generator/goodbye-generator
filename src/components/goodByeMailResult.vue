<template>
  <div class="letter">
    <div class="letterHead"></div>
    <div class="letterLeft"></div>
    <div class="letterBody">
      <p v-if="step">{{questions.name}} {{titleList[questions.title-1]}}</p>
      <template v-for="(results, questionNumber) in resultsList">
        <p v-if="step > questionNumber+1" :key="questionNumber">
          <template v-for="(result, resultIndex) in results">
            <span
              :key="result"
              v-if="questions[`q${questionNumber+1}`] === resultIndex+1"
            >{{result}}</span>
          </template>
        </p>
      </template>
    </div>
    <div class="letterRight"></div>
    <br>
    <div class="letterFoot"></div>
    <br>
  </div>
</template>

<script>
export default {
  props: {
    questions: Object,
    step: Number
  },
  computed: {
    titleList() {
      return ["さま", "様", "殿", "さん", "くん", "ちゃん"];
    },
    resultsList() {
      if (this.questions.sex == 0) {
        return [
          [
            "マイケルジャクソンのテレビみた？",
            "このまえはおみやげどうもありがとう。",
            "花粉症の調子はどうですか？。",
            "…………。"
          ],
          [
            "あなたにお話したいことがあります。",
            "１回しか言わないからよく聞いておけよー",
            "ねえ。きいて。ねえ、聞いてよ。",
            "………。ああ……。う、う、う。"
          ],
          [
            "私たち、別れましょう。",
            "あなたとはもう会わないようにしましょう。",
            "ほかに好きな人ができました。。",
            "ワカレルノダー"
          ],
          [
            "あなたが二重を自慢するのが嫌でした。",
            "私はひどい人間だから。あなたの本を勝手にブックオフに売るし。",
            "だって、くさいから。",
            "私、ロボットなんです。"
          ],
          [
            "貸してた本はあげますから。",
            "あなたに貸した本、私だと思って読んでください。",
            "貸していた本は、大変お手数ですが、下記までご送付ください。なお、送料はご負担ください。",
            "貸してた本だけど、くさいからいらないからね。"
          ],
          [
            "では。さよなら。",
            "いままでどうもありがとう。楽しかったです。幸せを祈ってます。",
            "でも、嫌いになったわけじゃないから。ではでは。",
            "ああ、くさかった。"
          ]
        ];
      } else {
        return [
          [
            "こんにちは！",
            "ごきげんいかが、ハニー。",
            "きのう、きみの夢を見たよ。",
            "携帯の番号変えたの？"
          ],
          [
            "あらたまって手紙だなんて照れるよね。",
            "きみからのメールももうすぐ100通。",
            "いつも電話だけど、こういうのもいいよね。",
            "いつもあなたを見てました。"
          ],
          [
            "おれたち、別れよう。",
            "僕らの関係も卒業さ。",
            "今年の花見はいっしょにいけないよ。",
            "ブエノスアイレスに行くことになりました。もう会えない。"
          ],
          [
            "おまえの愛におれはこたえられない。自信がないんだ。",
            "おまえはおれじゃなくて、テレビに出て歌ったり踊ったりしてるおれが好きなんだろ？",
            "ドラクエ、おれの続きをやっただろ。楽しみにしてたのに。もう終わりだ。",
            "だって、メガネかけてくれないんだもん！"
          ],
          [
            "きみに貸してるCD はオークションにでも出してくれ。",
            "きみに貸したCD は砂に埋めてくれ。僕の記憶といっしょに………。",
            "あ、おまえに貸したCD さあ、あげるけど、CD-R に焼いておれに送ってくんない？",
            "あ、貸してたCD だけどさ、ハトだらけのおまえの家のベランダにぶら下げろよ。"
          ],
          [
            "ということでさようなら。ありがとね。",
            "おまえはいい女、すぐに新しい男（ひと）見つかるさ………。",
            "生まれ変わったらいっしょになろうね。じゃ。",
            "最後に言っとくけど、きみがスタバって呼んでたあの店、ドトールだから。じゃあね。"
          ]
        ];
      }
    }
  },
  methods: {}
};
</script>

<style scoped>
.letter {
  border-top: dotted 1px #c6c6c6;

  line-height: 0px;
  margin: 0px;
  margin-top: 20px;
  padding: 0px;
  padding-top: 20px;

  width: 484px;
  height: 442px;
}

.letterLeft {
  float: left;
  width: 54px;
  height: 356px;
  background-image: url("../assets/letter_left.jpg");
  background-repeat: no-repeat;
  background-position: top, center;
}
.letterRight {
  float: left;
  width: 61px;
  height: 356px;
  background-image: url("../assets/letter_right.jpg");
  background-repeat: no-repeat;
  background-position: top, center;
}

.letterBody {
  line-height: 100%;
  font-size: 12pt;

  float: left;
  width: 369px;
  height: 356px;
  margin: 0px;
  padding: 0px;
  background-image: url("../assets/letter_back.jpg");
  background-repeat: no-repeat;
  background-position: top, center;
}

.letterHead {
  width: 484px;
  height: 43px;
  background-image: url("../assets/letter_head.jpg");
  background-repeat: no-repeat;
  background-position: top, center;
}

.letterFoot {
  float: left;
  width: 484px;
  height: 43px;
  background-image: url("../assets/letter_foot.jpg");
  background-repeat: no-repeat;
  background-position: top, center;
}
</style>