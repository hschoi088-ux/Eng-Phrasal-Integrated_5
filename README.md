
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>스피드 영어 퀴즈 (Week 5~8)</title>
    <style>
        body {
            font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, system-ui, Roboto, sans-serif;
            background-color: #f0f4f8;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 20px;
            box-sizing: border-box;
        }
        .container {
            background: white;
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.08);
            max-width: 650px;
            width: 100%;
        }
        h1 { text-align: center; margin-bottom: 20px; color: #1e293b; font-size: 26px; }
        
        /* Week 탭 스타일 */
        .week-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 10px;
            justify-content: center;
            flex-wrap: wrap;
        }
        .week-tab {
            padding: 10px 16px;
            border: none;
            background: none;
            font-size: 15px;
            font-weight: bold;
            color: #94a3b8;
            cursor: pointer;
            border-radius: 8px;
            transition: all 0.2s;
        }
        .week-tab.active {
            background-color: #e0f2fe;
            color: #0284c7;
        }
        .week-tab:hover:not(.active) { background-color: #f1f5f9; }

        /* 카테고리 영역 */
        .category-section {
            margin-bottom: 25px;
            background: #f8fafc;
            padding: 20px;
            border-radius: 12px;
            border: 1px solid #e2e8f0;
        }
        .category-title {
            font-size: 18px; font-weight: bold; color: #334155;
            margin-top: 0; margin-bottom: 15px; display: flex; align-items: center; gap: 8px;
        }
        
        /* 순한맛 / 매운맛 버튼 */
        .flavor-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; }
        @media (max-width: 480px) { .flavor-grid { grid-template-columns: 1fr; } }
        .flavor-btn {
            background: white; border: 2px solid #cbd5e1; border-radius: 10px;
            padding: 15px; text-align: left; cursor: pointer; transition: all 0.2s ease;
        }
        .flavor-btn:hover { border-color: #3b82f6; box-shadow: 0 4px 12px rgba(59, 130, 246, 0.15); transform: translateY(-2px); }
        .flavor-title { font-size: 16px; font-weight: bold; display: block; margin-bottom: 6px; }
        .flavor-desc { font-size: 13px; color: #64748b; line-height: 1.4; word-break: keep-all; }
        .t-easy { color: #10b981; } .t-hard { color: #ef4444; }
        .hidden { display: none !important; }
        
        /* 퀴즈 영역 스타일 */
        #quiz-area { display: flex; flex-direction: column; gap: 20px; }
        #question-counter { font-size: 15px; color: #64748b; font-weight: bold; text-align: center;}
        
        .question-box { 
            font-size: 22px; font-weight: bold; word-break: keep-all; line-height: 1.5; 
            background: #f8fafc; padding: 30px 20px; border-radius: 12px;
            border: 2px dashed #cbd5e1; cursor: pointer; transition: background 0.2s; text-align: center;
        }
        .question-box:hover { background: #e2e8f0; }
        .question-box::after { content: "(클릭하여 정답 확인)"; font-size: 13px; color: #94a3b8; display: block; margin-top: 10px; font-weight: normal; }

        .answer-box { 
            background: #ecfdf5; padding: 25px 20px; border-radius: 12px; border: 1px solid #a7f3d0; text-align: left;
        }
        .en-text { font-size: 22px; color: #059669; font-weight: bold; margin-bottom: 15px; line-height: 1.4; word-break: keep-all;}
        .meta-info { font-size: 14px; color: #475569; margin-bottom: 5px; background: #fff; display: inline-block; padding: 4px 10px; border-radius: 20px; border: 1px solid #e2e8f0; }
        .meaning-info { font-size: 15px; color: #b45309; margin-bottom: 15px; background: #fef3c7; padding: 8px 12px; border-radius: 8px; font-weight: 500;}
        
        .controls { display: flex; justify-content: space-between; align-items: center; margin-top: 10px; flex-wrap: wrap; gap: 10px;}
        .left-controls { display: flex; gap: 10px; }
        
        /* 버튼 스타일 */
        .btn { padding: 10px 20px; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 15px; transition: 0.2s;}
        .btn-tts { background-color: #8b5cf6; color: white; display: flex; align-items: center; gap: 5px; }
        .btn-tts:hover { background-color: #7c3aed; }
        .btn-star { background-color: #e2e8f0; color: #475569; }
        .btn-star.active { background-color: #fef08a; color: #ca8a04; border: 1px solid #fde047; }
        .btn-next { background-color: #10b981; color: white; }
        .btn-next:hover { background-color: #059669; }
        .btn-finish { background-color: #3b82f6; color: white; width: 100%; padding: 15px; font-size: 16px; margin-top: 10px; }
        .btn-finish:hover { background-color: #2563eb; }
        .btn-home { background-color: #64748b; color: white; width: 100%; padding: 15px; font-size: 16px; margin-top: 20px;}
        .btn-home:hover { background-color: #475569; }

        /* 복습(결과) 영역 스타일 */
        #review-area { display: flex; flex-direction: column; gap: 15px; }
        .review-card { background: #fff; border: 1px solid #e2e8f0; border-radius: 10px; padding: 15px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); text-align: left;}
        .review-ko { font-size: 16px; font-weight: bold; color: #334155; margin-bottom: 8px; }
        .review-en { font-size: 18px; font-weight: bold; color: #059669; margin-bottom: 8px; }
        .review-empty { text-align: center; padding: 40px 20px; font-size: 18px; color: #10b981; font-weight: bold; background: #ecfdf5; border-radius: 12px;}
    </style>
</head>
<body>

<div class="container">
    <h1 id="main-title">🚀 스피드 영어 퀴즈</h1>
    
    <div id="mode-selection">
        <div class="week-tabs">
            <button class="week-tab active" onclick="setWeek(5, this)">Week 5</button>
            <button class="week-tab" onclick="setWeek(6, this)">Week 6</button>
            <button class="week-tab" onclick="setWeek(7, this)">Week 7</button>
            <button class="week-tab" onclick="setWeek(8, this)">Week 8</button>
            <button class="week-tab" onclick="setWeek('all', this)">Week 5~8 누적</button>
        </div>

        <div class="category-section">
            <h3 class="category-title">🧩 구동사 (Phrasal Verbs)</h3>
            <div class="flavor-grid">
                <button class="flavor-btn" onclick="startQuiz('phrasal-easy')">
                    <span class="flavor-title t-easy">🟢 순한맛</span>
                    <span class="flavor-desc">구동사 의미별로 짧고 쉬운 문장들이 선별해서 담겨있음</span>
                </button>
                <button class="flavor-btn" onclick="startQuiz('phrasal-hard')">
                    <span class="flavor-title t-hard">🔴 매운맛</span>
                    <span class="flavor-desc">전체 예문에서 선별됨</span>
                </button>
            </div>
        </div>

        <div class="category-section">
            <h3 class="category-title">🗣️ 영어회화 (Conversation)</h3>
            <div class="flavor-grid">
                <button class="flavor-btn" onclick="startQuiz('conv-easy')">
                    <span class="flavor-title t-easy">💬 순한맛</span>
                    <span class="flavor-desc">'대표문장'과 '교재1'만 담고 있음</span>
                </button>
                <button class="flavor-btn" onclick="startQuiz('conv-hard')">
                    <span class="flavor-title t-hard">🔥 매운맛</span>
                    <span class="flavor-desc">전체 예문에서 선별됨</span>
                </button>
            </div>
        </div>
    </div>

    <div id="quiz-area" class="hidden">
        <div id="question-counter">문제 1 / 7</div>
        
        <div class="question-box" id="ko-box" onclick="showAnswer()">
            <span id="ko-text">한국어 문장이 여기에 표시됩니다.</span>
        </div>

        <div class="answer-box hidden" id="answer-section">
            <div class="meta-info" id="source-info">출처: Day001 교재1</div>
            <div class="en-text" id="en-text">English Answer</div>
            <div class="meaning-info hidden" id="meaning-info">의미: </div>
            
            <div class="controls">
                <div class="left-controls">
                    <button class="btn btn-tts" onclick="playTTS()">🔊 듣기</button>
                    <button class="btn btn-star" id="btn-star" onclick="toggleStar()">⭐ 어려워요</button>
                </div>
                <button class="btn btn-next" id="btn-next" onclick="nextQuestion()">다음 문제 ➡</button>
            </div>
        </div>

        <button class="btn btn-finish hidden" id="btn-finish" onclick="showReview()">결과 보기 (오답 노트) 📝</button>
    </div>

    <div id="review-area" class="hidden">
        <h2 style="text-align: center; color: #1e293b; margin-top:0;">⭐ 나의 오답 노트</h2>
        <p style="text-align: center; color: #64748b; font-size: 14px; margin-top:-10px;">어려웠던 문장들을 다시 확인해 보세요!</p>
        
        <div id="review-list"></div>

        <button class="btn btn-home" onclick="resetToHome()">🏠 처음으로 돌아가기</button>
    </div>
</div>

<script>
    let currentWeekFilter = 5; // ★ Week 5~8용 페이지이므로 기본값을 5로 변경

    function setWeek(week, btn) {
        currentWeekFilter = week;
        document.querySelectorAll('.week-tab').forEach(el => el.classList.remove('active'));
        btn.classList.add('active');
    }

    // 📌 구동사 Week 5 의미 매핑
    const meanings = {
        "find out_1": "find out: (조사나 질문을 통해 몰랐던) 정보를 알아내다",
        "fit in_1": "fit in: (디자인이나 분위기가 주변과) 조화를 이루다",
        "fit in_2": "fit in: (새로운 그룹이나 공동체에) 위화감 없이 적응하다",
        "fit in_3": "fit in: (좁은 공간이나 빽빽한 일정 사이에) 짬을 내어 끼워넣다",
        "get around_1": "get around: (여러 곳을) 돌아다니다, 이동하다",
        "get around_2": "get around: (신체적 불편함을 극복하고) 혼자서 다니다",
        "get around_3": "get around: (소문이나 소식이) 사람들에게 널리 알려지다",
        "get around_4": "get around: (사교 모임 등에) 활발하게 활동하며 다니다",
        "get around_5": "get around: (교묘하게 규정이나 법망을) 피해 가다",
        "get around_6": "get around: (인정하고 싶지 않은 사실을) 부인하거나 회피하다",
        "get around to_1": "get around to: (시간이 없어서 미뤄왔던 일을) 마침내 짬을 내어 하다"
    };

    // 1. 구동사 순한맛 (현재 Week 5만 포함)
    const phrasalEasy = [
        { week: 5, ko: "영화관에 뭐 상영하고 있는지 한번 알아보자.", en: "Let’s find out what’s playing at the movie theater.", source: "Day 021 순한맛", meaning: meanings["find out_1"] },
        { week: 5, ko: "빨강은 우리 집 거실의 차분한 분위기와는 따로 놀 테니까.", en: "Red doesn’t fit in with the living room’s calm vibe.", source: "Day 022 순한맛", meaning: meanings["fit in_1"] },
        { week: 5, ko: "나는 늘 겉도는 느낌이었거든.", en: "I never truly felt like I fit in.", source: "Day 022 순한맛", meaning: meanings["fit in_2"] },
        { week: 5, ko: "요즘 너무 바빠서 운동할 짬도 안 납니다.", en: "I have been too busy to fit a workout in.", source: "Day 022 순한맛", meaning: meanings["fit in_3"] },
        { week: 5, ko: "새 자전거도 마련했으니 동네를 쉽게 돌아다닐 수 있겠군.", en: "Now that I got a new bike, I can easily get around the neighborhood.", source: "Day 023 순한맛", meaning: meanings["get around_1"] },
        { week: 5, ko: "Mobility devices 덕분에 몸이 불편한 분들도 혼자서 다닐 수 있다.", en: "Mobility devices allow disabled individuals to get around independently.", source: "Day 023 순한맛", meaning: meanings["get around_2"] },
        { week: 5, ko: "Nick이 결혼한다는 소문이 사무실에 쫙 퍼졌다.", en: "Word got around the office that Nick was getting married.", source: "Day 023 순한맛", meaning: meanings["get around_3"] },
        { week: 5, ko: "와, 너 정말 여기저기 많이 다니는구나.", en: "Wow, you certainly get around.", source: "Day 024 순한맛", meaning: meanings["get around_4"] },
        { week: 5, ko: "일부 기업들은 법을 지키지 않으려고 늘 허점을 찾는다.", en: "Some companies are always looking for loopholes to get around the law.", source: "Day 024 순한맛", meaning: meanings["get around_5"] },
        { week: 5, ko: "요즘 집 사는 데 돈이 많이 든다는 점은 부인할 수 없는 사실이다.", en: "There’s no getting around the fact that buying a house is expensive.", source: "Day 024 순한맛", meaning: meanings["get around_6"] },
        { week: 5, ko: "드디어 내 차 엔진 오일을 갈았어.", en: "I finally got around to changing the oil in my car.", source: "Day 025 순한맛", meaning: meanings["get around to_1"] }
    ];

    // 2. 구동사 매운맛 (현재 Week 5만 포함)
    const phrasalHard = [
        { week: 5, ko: "그 선생님의 강의 스타일과 가능한 시간대에 대해 좀 더 알고 싶습니다.", en: "I was hoping to find out more about his teaching style and his availability.", source: "Day 021 교재3", meaning: meanings["find out_1"] },
        { week: 5, ko: "역에 도착해 보니 엉뚱한 날짜의 표를 예매했더라고요.", en: "When we got to the station, we found out that we had booked tickets for the wrong day.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "이 대학의 경우 지원 절차가 좀 느립니다. 그래서 합격 여부를 알려면 몇 주 더 기다려야 합니다.", en: "The application process is pretty slow for this university. I’ll have to wait a couple more weeks to find out whether I’ve gotten in or not.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "너를 많이 좋아해. 하지만 결혼하기 전에 (우린) 서로에 대해 좀 더 알아야 해.", en: "I like you a lot, but we should find out more about each other before getting married.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "블랙핑크에 대해 알 수 있는 거의 모든 것을 알아봅시다.", en: "Let’s find out almost everything there is to know about BLACKPINK.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "그 사람이 그동안 저한테 나이를 속여 왔다는 걸 알게 되었어요.", en: "I just found out (that) he has been lying to me about his age.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "영화관에 뭐 상영하고 있는지 한번 알아보자.", en: "Let’s find out what’s playing at the movie theater.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "애당초 그 둘이 어디서 만났는지 알면 놀랄 거야. 이태원에 있는 클럽에서 만났는데 여자가 바텐더였어.", en: "You will be surprised to find out how they first met. It was actually at a club in Itaewon and she was the bartender.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "<베첼러>에 나오는 커플이 결혼에 골인할지 너무 궁금하다.", en: "I’m curious to find out if the couple on The Bachelor will actually get married.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "워크숍 연기 여부를 알아보기 위해 이메일을 확인해야 한다.", en: "I should check my e-mail to find out whether the workshop has been pushed back or not.", source: "Day 021 교재1", meaning: meanings["find out_1"] },
        { week: 5, ko: "죄송한데요. 어제 헬스장 갔다가 청소 때문에 휴관이라는 걸 알았어요. 이런 건 사전에 공지가 되어야 하지 않나요? 하루 계획이 엉망이 되었어요!", en: "Excuse me. I went to the gym yesterday and only then found out that it was closed for cleaning. Shouldn’t there have been advance notice? It really ruined my plans for the day!", source: "Day 021 교재2", meaning: meanings["find out_1"] },
        { week: 5, ko: "불편을 드려 죄송합니다. 하지만 지난주 마포구청 앱에 휴관 관련 공지가 있었습니다. 혹시 휴대폰에 앱을 깔아 두셨을까요?", en: "I’m sorry about the inconvenience. However, an announcement about the gym closure was made last week on the Mapo District app. Do you happen to have that on your phone?", source: "Day 021 교재2", meaning: null },
        { week: 5, ko: "무엇을 도와드릴까요?", en: "How may I help you?", source: "Day 021 교재2", meaning: null },
        { week: 5, ko: "사실 어제 작은 접촉 사고가 났어요. 차 수리 비용이 어느 정도일지 알고 싶어서 연락드렸습니다.", en: "I actually got in a little fender bender yesterday, so I wanted to find out how much it would cost to get my car fixed.", source: "Day 021 교재2", meaning: meanings["find out_1"] },
        { week: 5, ko: "Sarah랑 Tom이 사귀게 되었다는 거 들었어? 어떻게 둘이 죽이 잘 맞게 되었는지 정말 궁금하네.", en: "Have you heard that Sarah and Tom are a thing now? I really want to find out how they hit it off.", source: "Day 021 교재2", meaning: meanings["find out_1"] },
        { week: 5, ko: "정말? 나는 너무 잘 어울린다고 늘 생각했는데. 지난 주말에 그 둘이 이태원에 춤추러 갔다고 들었어. 거기서 무슨 일이 있었을 거야.", en: "Really? I always thought they’d make a great couple. I heard they both went out clubbing in Itaewon last weekend. Maybe something happened there.", source: "Day 021 교재2", meaning: null },
        { week: 5, ko: "안녕, 얘들아. 그래서… 내일 저녁에 뭐 먹을지는 결정했어?", en: "Hey, guys. So… have we decided what we’re going to eat tomorrow night?", source: "Day 021 교재3", meaning: null },
        { week: 5, ko: "종로에 가 보고 싶은 이탈리아 음식점이 있는데, 네이버에는 메뉴가 안 나와 있네. 전화해서 무슨 메뉴가 있는지 물어봐야겠다.", en: "There’s this Italian restaurant in Jongno that I’m curious about, but I don’t see any of their dishes listed on Naver. I guess I’ll have to call them to find out what’s on their menu.", source: "Day 021 교재3", meaning: meanings["find out_1"] },
        { week: 5, ko: "잘됐네! 안 그래도 며칠 전부터 이탈리아 음식이 먹고 싶었는데.", en: "Perfect! I’ve been craving Italian food for the past few days.", source: "Day 021 교재3", meaning: null },
        { week: 5, ko: "잘 들어 봐. 방금 전화해서 확인해 봤는데 내일이랑 모레 이틀간 전 메뉴 20% 할인이래!", en: "Get this – I just called to check, and they said everything is 20% off for the next two days!", source: "Day 021 교재3", meaning: null },
        { week: 5, ko: "좋은 넥타이긴 한데 동생이 가지고 있는 다른 것들이랑 좀 안 맞아.", en: "It’s a nice tie, but it doesn’t really fit in with my brother’s collection.", source: "Day 022 교재1", meaning: meanings["fit in_1"] },
        { week: 5, ko: "내가 어떻게 2년이나 그 직장에 다녔는지 모르겠어. 나는 늘 겉도는 느낌이었거든.", en: "I can’t believe I stayed at that workplace for two whole years. I never truly felt like I fit in.", source: "Day 022 교재1", meaning: meanings["fit in_2"] },
        { week: 5, ko: "SUV 구매는 제 라이프스타일과 맞지 않습니다. 제가 다른 사람을 태우고 다니는 일도 많지 않고, 많이 다니지도 않으며, 야외 활동을 그렇게 많이 하지도 않거든요.", en: "Buying an SUV doesn’t fit in with my lifestyle because I don’t often have passengers, and I don’t get out and do outdoor activities very much.", source: "Day 022 교재1", meaning: meanings["fit in_1"] },
        { week: 5, ko: "여긴 경차 주차 공간인 것 같아. 들어갈 수 있는 공간이 충분한 것 같아?", en: "I think this is a space for compact cars. Do you really think you have enough space to fit in?", source: "Day 022 교재1", meaning: meanings["fit in_3"] },
        { week: 5, ko: "빨간색 쿠션은 너무 튈 것 같아. 빨강은 우리 집 거실의 차분한 분위기와는 따로 놀 테니까.", en: "I’m afraid the red cushion stands out because red doesn’t fit in with the living room’s calm vibe.", source: "Day 022 교재1", meaning: meanings["fit in_1"] },
        { week: 5, ko: "중학교 때는 매 학기 초에 적응하는 데 늘 애를 먹었어요.", en: "Back in middle school, I always had trouble fitting in early on in the semester.", source: "Day 022 교재1", meaning: meanings["fit in_2"] },
        { week: 5, ko: "기념품을 너무 많이 샀어. 여행 가방에 다 안 들어갈 것 같아.", en: "I bought way too many souvenirs. I don’t think I can fit all this stuff in my suitcase.", source: "Day 022 교재1", meaning: meanings["fit in_3"] },
        { week: 5, ko: "요즘 너무 바빠서 운동할 짬도 안 납니다.", en: "I have been too busy to fit a workout in (my schedule).", source: "Day 022 교재1", meaning: meanings["fit in_3"] },
        { week: 5, ko: "Samantha가 그만둔다는 이야기 들었어요? 이미 사직서를 제출했대요.", en: "Did you hear Samantha is leaving? She already turned in her resignation.", source: "Day 022 교재2", meaning: null },
        { week: 5, ko: "그만두는 게 당연할지도요. 이럴 줄 알았어요. 어쨌든 이 회사에서 늘 겉돌았잖아요.", en: "It’s no surprise she’s leaving. I actually saw this coming. She never really fit in, after all.", source: "Day 022 교재2", meaning: meanings["fit in_2"] },
        { week: 5, ko: "... 그럼 이 덴마크산 가죽 소파를 추천해 드립니다. 추가 혜택으로 이번 주에 한해 15% 세일도 하거든요.", en: "... then I would recommend this Danish leather couch. As an added bonus, it’s actually on sale for 15% off, this week only.", source: "Day 022 교재2", meaning: null },
        { week: 5, ko: "가구의 경우 덴마크산이 진리이긴 하죠. 근데 가죽 소파는 제가 추구하는 저희 집의 아늑한 분위기와는 따로 놀 것 같아서요.", en: "I know you can’t go wrong with Danish craftsmanship when it comes to furniture, but I’m afraid a leather couch wouldn’t fit in with the cozy vibe I’m going for at my place.", source: "Day 022 교재2", meaning: meanings["fit in_1"] },
        { week: 5, ko: "다음 달 마라톤에 출전하기 전에 Thompson 박사님을 뵙고 무릎 진료를 받고 싶습니다. 혹시 진료 가능한 시간 있을까요?", en: "I’d really like to see Dr. Thompson about my knee before the marathon next month. Are there any openings available?", source: "Day 022 교재2", meaning: null },
        { week: 5, ko: "선생님께서 꽤 바쁘십니다. 언제 가능할지 스케줄 확인해 드릴게요. 마라톤을 앞두고 좋은 몸 상태를 유지하시는 게 중요한 점 알고 있습니다.", en: "She’s been quite busy, but let me check her schedule to see when she can fit you in. I understand it is important for you to be in good shape for the race.", source: "Day 022 교재2", meaning: meanings["fit in_3"] },
        { week: 5, ko: "골프는 나랑 진짜 안 맞다.", en: "Playing golf isn’t really for me.", source: "Day 022 교재3", meaning: null },
        { week: 5, ko: "뭔가 모르게 재미가 안 붙는다.", en: "For some reason, I just can’t get into it.", source: "Day 022 교재3", meaning: null },
        { week: 5, ko: "내게 골프는 스포츠가 아닌 게임이다.", en: "I think of it as a game, not a sport.", source: "Day 022 교재3", meaning: null },
        { week: 5, ko: "하지만 영업직이다 보니 (사람들과) 어울리기 위해서는 골프를 시작할 수밖에 없었다.", en: "Working in sales, though, I had to take up golf just to fit in.", source: "Day 022 교재3", meaning: meanings["fit in_2"] },
        { week: 5, ko: "솔직히 토요일 아침 일찍 일어나는 게 너무 싫지만 그래도 어쩌겠나.", en: "Honestly, I dread waking up early on Saturday mornings, but it is what it is.", source: "Day 022 교재3", meaning: null },
        { week: 5, ko: "사실 내게 골프는 선택의 문제가 아닌 인맥 유지의 수단이다.", en: "Actually, for me, playing golf is not an option, but a means for networking.", source: "Day 022 교재3", meaning: null },
        { week: 5, ko: "그래도 야외에서 인맥을 쌓을 수 있어서 감사해야 할 것 같다. (사람들과) 이야기도 나누고 신선한 공기도 마실 수 있으니 말이다.", en: "I suppose I should be grateful that I can network outdoors, where it’s easy to talk and get some fresh air.", source: "Day 022 교재3", meaning: null },
        { week: 5, ko: "다만 내가 골프를 조금만 더 좋아했어도 좋으련만.", en: "But I just wish I enjoyed golf a bit more.", source: "Day 022 교재3", meaning: null },
        { week: 5, ko: "새 자전거도 마련했으니 동네를 쉽게 돌아다닐 수 있겠군.", en: "Now that I got a new bike, I can easily get around the neighborhood.", source: "Day 023 교재1", meaning: meanings["get around_1"] },
        { week: 5, ko: "저희 할아버지는 91세이신데도 여전히 (여기저기) 잘 다니십니다.(= 외출하시는데 문제가 없습니다.)", en: "My grandpa is 91, but he still gets around well.", source: "Day 023 교재1", meaning: meanings["get around_2"] },
        { week: 5, ko: "Taylor Swift가 도착한다는 소식이 빠르게 알려졌고, 공항에서 수백 명의 열혈 팬들이 그녀를 맞이했다.", en: "Word got around fast about the arrival of Taylor Swift, and she was met at the airport by hundreds of eager fans.", source: "Day 023 교재1", meaning: meanings["get around_3"] },
        { week: 5, ko: "디지털 노마드인 Sarah는 이 나라 저 나라를 (돌아) 다닌다.", en: "As a digital nomad, Sarah gets around by hopping from one country to another.", source: "Day 023 교재1", meaning: meanings["get around_1"] },
        { week: 5, ko: "모빌리티 디바이스(개인용 이동 수단) 덕분에 몸이 불편한 분들도 혼자서 다닐 수 있다.", en: "Mobility devices allow disabled individuals to get around independently.", source: "Day 023 교재1", meaning: meanings["get around_2"] },
        { week: 5, ko: "Nick이 결혼한다는 소문이 사무실에 쫙 퍼졌다.", en: "Word got around the office that Nick was getting married.", source: "Day 023 교재1", meaning: meanings["get around_3"] },
        { week: 5, ko: "최근에 사무실 주변에 주차 공간 찾기가 이렇게 어렵다니 말이 돼? 아예 차를 완전히 버리고 자전거로 다녀야 할까 봐.", en: "Can you believe how difficult it is to find parking near the office lately? I’m considering ditching my car altogether and using a bike to get around.", source: "Day 023 교재2", meaning: meanings["get around_1"] },
        { week: 5, ko: "정말? 그것도 괜찮은 생각이다. 난 지난달에 주차 위반 딱지를 세 번이나 끊겼어. (차 안 가지고 다니면) 돈도 절약할 수 있겠네.", en: "Really? That’s not a bad idea. I got three parking tickets last month. You might save some money, too.", source: "Day 023 교재2", meaning: null },
        { week: 5, ko: "Dereck, 시내에 새로 생긴 쇼핑몰에서 만나서 저녁 먹을까?", en: "Hey, Dereck, why don’t we meet at the new mall downtown for dinner?", source: "Day 023 교재2", meaning: null },
        { week: 5, ko: "지난번에 거기 갔을 때 통로가 너무 좁아서 휠체어 타고 다니는 데 애를 먹었어. 이동이 쉬운 곳에 가 보는 게 어떨까?", en: "Last time I went there I had trouble getting around the narrow aisles in my wheelchair. Could we try a place with better accessibility?", source: "Day 023 교재2", meaning: meanings["get around_2"] },
        { week: 5, ko: "Samantha가 동네방네 깜짝파티를 떠벌리고 다녔다네.", en: "I heard Samantha blabbed about the surprise party to everyone.", source: "Day 023 교재2", meaning: null },
        { week: 5, ko: "하이고, 이제 Peter한테 이야기가 들어가서 깜짝파티 다 들통나겠어!", en: "Ugh, now it’s definitely going to get around to Peter and spoil his surprise!", source: "Day 023 교재2", meaning: meanings["get around_3"] },
        { week: 5, ko: "지은아, 발리 여행은 어땠어? 발리에서는 어떻게 다녔어?", en: "Hey, Jieun, how was Bali? How did you get around on the island?", source: "Day 023 교재3", meaning: meanings["get around_1"] },
        { week: 5, ko: "무슨 일이 있었는지 알면 믿기지 않을 거야. ‘택시 문제’로 아주 난리였어. 거기 택시 기사들 대부분이 정말 제멋대로더라고. 관광객들에게 바가지를 씌우려고 했거든.", en: "You won’t believe what happened. We had a lot of “taxi drama.” Most of the taxi drivers there have become so spoiled, trying to rip off tourists.", source: "Day 023 교재3", meaning: null },
        { week: 5, ko: "정말?", en: "Really?", source: "Day 023 교재3", meaning: null },
        { week: 5, ko: "응. 어떤 택시 기사는 팁을 안 줬다고 남편에게 소리를 질렀어. 너무 화가 나서 경찰을 부르려고 했는데, 다행히 지역 주민들이 개입해서 나를 말렸지.", en: "Yeah, this taxi driver yelled at my husband for not tipping. I was so angry. I was ready to call the police, but thankfully, the locals stepped in and talked me out of it.", source: "Day 023 교재3", meaning: null },
        { week: 5, ko: "끔찍하다.", en: "That sounds awful.", source: "Day 023 교재3", meaning: null },
        { week: 5, ko: "응. 택시와 관련된 이런 안 좋은 경험이 여행 전체를 망쳐 버렸어.", en: "Yeah, those unpleasant experiences with the taxis ruined our entire trip.", source: "Day 023 교재3", meaning: null },
        { week: 5, ko: "저희 어머니가 70대 후반인데도 저보다 더 활동적입니다. 늘 지역 사회 행사에 참여하셔서 자원봉사를 하십니다. 정말 대단하다고 생각됩니다.", en: "My mom is in her late 70s, but she still gets around more than I do. She’s always attending and volunteering at community events. I really admire that.", source: "Day 024 교재1", meaning: meanings["get around_4"] },
        { week: 5, ko: "A: Kevin, 새 직장은 어때?", en: "A: Kevin, how’s the new job?", source: "Day 024 교재1", meaning: null },
        { week: 5, ko: "B: 바빠. 영업팀 소속이라 주 5회씩 밤에 이런저런 모임과 행사에 참석하거든.", en: "B: Busy. I’m on the sales team and we get around to some kind of social function five nights a week!", source: "Day 024 교재1", meaning: meanings["get around_4"] },
        { week: 5, ko: "세금 안 낼 생각은 하지도 마. 반드시 걸리게 되어 있어.", en: "Don’t even think of trying to get around paying taxes. You would never get away with it.", source: "Day 024 교재1", meaning: meanings["get around_5"] },
        { week: 5, ko: "엔지니어는 안이하게 배움을 멈추면 안 된다. 신기술에 뒤처지지 않으려면 지속적인 커리어 개발을 피할 수 없다.", en: "You can’t just relax and stop learning as an engineer. There’s no getting around the continuous professional development to keep up with new technology.", source: "Day 024 교재1", meaning: meanings["get around_6"] },
        { week: 5, ko: "일부 기업들은 법을 지키지 않으려고 늘 (법의) 허점을 찾는다.", en: "Some companies are always looking for loopholes to get around the law.", source: "Day 024 교재1", meaning: meanings["get around_5"] },
        { week: 5, ko: "나이 드는 것을 피하고 부정할 수는 없어. 우리 모두가 겪는 일이니까.", en: "There’s no getting around getting older. It happens to us all.", source: "Day 024 교재1", meaning: meanings["get around_6"] },
        { week: 5, ko: "A: 한번 들어 봐. 월요일에는 골프장에 갔어. 화요일에는 회의차 부산에 갔지. 수요일에는 여러 저녁 모임 때문에 서울에 다시 올라왔어. 그리고 내일은 추가 회의 때문에 뉴욕에 가.", en: "A: Listen to this: Monday, I was on the golf course. Tuesday, I was in Busan for a conference. Wednesday, I was back in Seoul for multiple dinner gatherings. Then tomorrow, I’m flying out to New York for more meetings.", source: "Day 024 교재1", meaning: null },
        { week: 5, ko: "B: 와, 너 정말 여기저기 많이 다니는구나.", en: "B: Wow, you certainly get around.", source: "Day 024 교재1", meaning: meanings["get around_4"] },
        { week: 5, ko: "어떤 날 아침에는 정말 청소하기가 싫다. 그래서 (회사에) 늦은 척하며 설거지하는 걸 피해 버린다. 아내가 하도록 싱크대 옆에 두고는 조용히 출근하러 나가 버린다. 이러면 정말 머저리가 된다는 걸 나도 안다.", en: "Some mornings, I really don’t feel like cleaning, so I get around doing the dishes by pretending I’m late. I leave them by the sink for my wife to do and quietly head out to work. I know that makes me kind of a jerk.", source: "Day 024 교재1", meaning: meanings["get around_5"] },
        { week: 5, ko: "요즘 집 사는 데 돈이 많이 든다는 점은 부인할 수 없는 사실이다.", en: "There’s no getting around the fact that buying a house is expensive.", source: "Day 024 교재1", meaning: meanings["get around_6"] },
        { week: 5, ko: "최근에 Nick 봤어?", en: "Have you seen Nick lately?", source: "Day 024 교재2", meaning: null },
        { week: 5, ko: "응, 그 친구 이번 주에는 매일 밤 외출하더라. 여기저기 정말 많이 다녀.", en: "Oh yeah, he’s been out every night this week. He certainly gets around.", source: "Day 024 교재2", meaning: meanings["get around_4"] },
        { week: 5, ko: "Jeff, 나한테 <뉴욕타임스> 기사 계속 보내는구나. 페이월이 있을 텐데. 구독하는 거야?", en: "Jeff, you keep sending me these New York Times articles. They have a paywall. Do you subscribe to them?", source: "Day 024 교재2", meaning: null },
        { week: 5, ko: "아, 앱을 쓰는데 이걸 쓰면 페이월을 피할 수 있어. 여기 링크 보낼게. 한번 봐 봐.", en: "Oh, I use an app that allows me to get around paywalls. Here’s the link. Check it out.", source: "Day 024 교재2", meaning: meanings["get around_5"] },
        { week: 5, ko: "최근에 안 오르는 게 없군. 자장면까지.", en: "The prices of everything keep going up lately. Even jajangmyeon.", source: "Day 024 교재2", meaning: null },
        { week: 5, ko: "누가 아니래. 인플레이션을 피해갈 수는 없지.", en: "That’s for sure. There’s no getting around inflation.", source: "Day 024 교재2", meaning: meanings["get around_6"] },
        { week: 5, ko: "아, 몇 주간 위에 불편함이 계속 느껴져.", en: "Ugh, I’ve been feeling this discomfort in my stomach for weeks now.", source: "Day 024 교재3", meaning: null },
        { week: 5, ko: "어떡해. 병원에는 가 본 거야?", en: "That doesn’t sound good. Have you seen a doctor?", source: "Day 024 교재3", meaning: null },
        { week: 5, ko: "한 달 이상 통증을 그냥 무시하고는 있는데, 회피하면 안 될 듯해. 병원에 가 봐야 할 것 같아.", en: "I’ve been trying to ignore the pain for over a month now, but there’s no getting around it. I guess I do need to see one.", source: "Day 024 교재3", meaning: meanings["get around_6"] },
        { week: 5, ko: "맞아, Mark. 더 늦기 전에 서둘러서 검사를 받아 보는 게 좋을 거야.", en: "You’re right, Mark. It’s better to get it checked out sooner rather than later.", source: "Day 024 교재3", meaning: null },
        { week: 5, ko: "알아. 계속 미뤄 왔거든. 더 이상은 그냥 넘길 수가 없어.", en: "I know. I’ve been putting it off, but I just can’t ignore it any longer.", source: "Day 024 교재3", meaning: null },
        { week: 5, ko: "필요하면 내가 태워 줄게.", en: "I’ll give you a ride if you need it.", source: "Day 024 교재3", meaning: null },
        { week: 5, ko: "고마워. 나 자신을 좀 더 잘 챙겨야 할 듯해.", en: "Thanks. I appreciate it. I guess I need to take better care of myself.", source: "Day 024 교재3", meaning: null },
        { week: 5, ko: "드디어 내 차 엔진 오일을 갈았어. 이상한 소리가 나기 시작했거든.", en: "I finally got around to changing the oil in my car. It was starting to make strange noises.", source: "Day 025 교재1", meaning: meanings["get around to_1"] },
        { week: 5, ko: "제발 잔소리 좀 그만해. 쓰레기 내다 버린다고 내가 말했잖아. 시간 될 때 할게!", en: "Please stop nagging me. I already said I’ll take out the garbage. I’ll get around to it when I have time!", source: "Day 025 교재1", meaning: meanings["get around to_1"] },
        { week: 5, ko: "이건 ‘미뤘다가 할 수 있는 일’이 아니야. 파이프가 새는데 오늘 당장 고쳐야겠어!", en: "This isn’t something you can just “get around to.” That leaking pipe needs fixing today!", source: "Day 025 교재1", meaning: meanings["get around to_1"] },
        { week: 5, ko: "이제 진짜 네 방 청소해야 하지 않겠니?", en: "Don’t you think it’s about time you got around to cleaning your room?", source: "Day 025 교재1", meaning: meanings["get around to_1"] },
        { week: 5, ko: "이번 주에 크리스마스 카드 주문할 시간 되겠어? 아니면 내가 직접 주문할까?", en: "Do you think you can get around to ordering the Christmas cards this week? Or should I just go ahead and order them myself?", source: "Day 025 교재1", meaning: meanings["get around to_1"] },
        { week: 5, ko: "A: 이봐, 모네 전시회 언제 끝나는지 기억해? 몇 주째 보러 가기로 마음을 먹고 있잖아.", en: "A: Hey, do you remember when the Monet exhibit is over? We’ve been wanting to go see it for weeks.", source: "Day 025 교재1", meaning: null },
        { week: 5, ko: "B: 정확한 날짜는 모르겠어. 근데 얼마 남지 않았을 거야. 너무 늦기 전에 보러 가야 해.", en: "B: I’m not exactly sure of the date, but there must not be much time left. We should get around to seeing it before it’s too late.", source: "Day 025 교재1", meaning: meanings["get around to_1"] },
        { week: 5, ko: "그거 아직 안 한 거야? 새로 만든 쿠키 사진 찍은 거 올리는 거 말이야.", en: "Did you get around to it yet? I mean putting up the photos we took of our new cookies.", source: "Day 025 교재2", meaning: meanings["get around to_1"] },
        { week: 5, ko: "완전 깜박했어. 오늘 꼭 할 게. 요즘 왜 이렇게 정신이 없는지 모르겠어.", en: "I completely forgot. I swear I’ll do it today. I don’t know where my mind is these days.", source: "Day 025 교재2", meaning: null },
        { week: 5, ko: "드디어 이번 주에 세금 신고했어. 미루던 걸 하고 나니 속이 시원해.", en: "I finally got around to filing my taxes this week. It feels really nice to have gotten it over with.", source: "Day 025 교재2", meaning: meanings["get around to_1"] },
        { week: 5, ko: "잘했다! 그나저나 세금은 얼마를 내야 해? 환급이나 그런 거 받는 거야?", en: "That’s great! How much do you have to pay in taxes, by the way? Are you getting a refund or anything?", source: "Day 025 교재2", meaning: null },
        { week: 5, ko: "아홉 달째 치과 검진받으러 가야지 하고 있는데도 아직도 못 가고 있어.", en: "I have been meaning to go to the dentist for a checkup for, like, the last nine months, but I just haven’t gotten around to it.", source: "Day 025 교재2", meaning: meanings["get around to_1"] },
        { week: 5, ko: "안 돼. 치아 관리를 좀 더 잘해야 해. 정기적으로 치과에 가지 않으면 나중에 더 큰 문제가 생길 거야!", en: "No way. You should take better care of your teeth. If you don’t go to the dentist regularly, you’re going to have even bigger problems later!", source: "Day 025 교재2", meaning: null },
        { week: 5, ko: "지난주에 차에 타다가 아파트 카드 키를 운전석 아래쪽 손이 닿지 않는 곳에 떨어뜨렸다.", en: "Last week, I was getting in my car and I dropped my apartment key card somewhere beneath my driver’s seat where I can’t reach it.", source: "Day 025 교재3", meaning: null },
        { week: 5, ko: "(지금) 세차를 안 한 지 몇 달이나 되어서, 차 안이 좀 엉망이다. 그래서 카드 키를 찾기가 더 어렵다.", en: "I haven’t had my car washed for months, so the inside is a bit of a mess, making it even harder to find the card.", source: "Day 025 교재3", meaning: null },
        { week: 5, ko: "(이 정도면) 세차를 해야 할 이유가 충분한데도 아직 안 하고 있다.", en: "Now I have all the reason to take my car to the car wash, but still, I haven’t gotten around to it.", source: "Day 025 교재3", meaning: meanings["get around to_1"] },
        { week: 5, ko: "하려고 생각할 때마다 회사에 무슨 일이 생기거나, 그냥 하루를 더 미루게 된다.", en: "Every time I think about doing it, something else comes up at work or I just put it off for another day.", source: "Day 025 교재3", meaning: null },
        { week: 5, ko: "그래, 이번 주말에는 반드시 하기로 다짐한다. 더 이상의 핑계는 안 된다.", en: "Okay; I’m making a promise to myself to get it done this weekend. No more excuses.", source: "Day 025 교재3", meaning: null }
    ];

    // 3. 영어회화 데이터 (현재 Week 5만 포함)
    const rawConvData = [
        { week: 5, source: "Day021 교재1", ko: "그 친구는 저희가 진지하게 사귀는 관계인 줄 아는데, 저는 안 그렇거든요.", en: "She thinks we’re in a serious relationship, but I don’t see it that way." },
        { week: 5, source: "Day021 교재1", ko: "이 케이크 너무 달다고 그랬나? 안 그런 것 같은데.", en: "You said the cake is too sweet? I don’t see it that way." },
        { week: 5, source: "Day021 교재1", ko: "많은 사람들이 부동산 가격이 계속 하락할 거라고 생각하지만 제 생각은 다릅니다.", en: "Many people believe real estate prices will keep falling, but I don’t see it that way." },
        { week: 5, source: "Day021 교재1", ko: "일부 언론에서는 Elon Musk가 트위터를 망치고 있다고 하는데, 제 생각은 다릅니다.", en: "Some news agencies claim that Elon Musk is ruining Twitter, but I don’t see it that way." },
        { week: 5, source: "Day021 교재1", ko: "좋은 예문이긴 한데 출판사 생각은 다를 거라는 게 문제죠.", en: "I think that’s a great example, but the thing is, I don’t think the publisher is going to see it that way." },
        { week: 5, source: "Day021 교재2", ko: "우리 부모님은 늘 이렇게 가르치셨어. 노숙자를 도와주면 상황이 더 나빠진다고.", en: "My parents always taught me that supporting the homeless just makes the problem worse." },
        { week: 5, source: "Day021 교재2", ko: "나는 좀 생각이 다른데. 그들을 도와주면 그들의 삶이 더 나아질 거야.", en: "I don’t really see it that way. Supporting them could change their lives for the better." },
        { week: 5, source: "Day021 교재2", ko: "요즘 한국 출산율이 너무 낮아. 가정을 꾸리기에 알맞은 집을 마련하는 걸 감당할 수 없어서 그렇다고 봐. 좋은 집이 없으면, 어떻게 애들을 키우겠어?", en: "The birth rate in Korea is so low these days. I really think it’s because people can’t afford a proper house for a family. Without a good home, how could you raise kids?" },
        { week: 5, source: "Day021 교재2", ko: "좋은 지적이긴 한데, 내 생각은 좀 달라. 교육비가 너무 많이 들기 때문이라고 생각해.", en: "That’s a good point, but I don’t really see it that way. I think it’s because the cost of educating kids is too expensive." },
        { week: 5, source: "Day021 교재3", ko: "(CEO 인터뷰 내용)\n일부 전문가들은 저희가 사업을 온라인으로 전환해야 한다고 합니다. 특히, 비싼 시내 중심가에서 물리적인 사무실 공간을 임대하는 건 합리적이지 않다고들 합니다. 저는 그렇게 생각하지 않습니다. 직원들이 같은 공간에서 함께 일하게 될 때 업무 능률이 오르는 뭔가가 있습니다.", en: "Some experts say we should move business online. They argue that renting physical office space, especially in expensive downtown areas, doesn’t make any sense. I don’t see it that way. There is something about working together in the same room that helps employees stay productive." },
        { week: 5, source: "Day021 교재4", ko: "일리 있는 말씀입니다만…", en: "You’ve got a point there, but I actually..." },
        { week: 5, source: "Day021 교재4", ko: "왜 그런 말씀을 하시는지는 알겠습니다. 하지만 제 생각은 다릅니다.", en: "I see where you are coming from, but I had a different idea." },
        { week: 5, source: "Day021 교재4", ko: "그 점은 동의하기 힘듭니다.", en: "I’m not sure I agree with you on that." },
        { week: 5, source: "Day021 교재4", ko: "그 점에 있어서 동의하지는 않지만, 왜 그런 말을 하는지는 알 것 같네요.", en: "I don’t really agree with you on that, but I see where you are coming from." },
        { week: 5, source: "Day021 대표", ko: "제 생각은 좀 다릅니다.", en: "I don’t see it that way." },
        { week: 5, source: "Day022 교재1", ko: "제 월급으로 그 차를 살 수 있을지 모르겠네요.", en: "I’m not sure if I can afford that car on my salary." },
        { week: 5, source: "Day022 교재1", ko: "TV 큰 걸로 하자. 감당할 수 있어.", en: "Let’s go with the bigger TV. We can afford it." },
        { week: 5, source: "Day022 교재1", ko: "외식할 형편이 안 됩니다.", en: "We can’t afford to eat out." },
        { week: 5, source: "Day022 교재1", ko: "강남에 살 형편이 안 됩니다.", en: "I just can’t afford to live in Gangnam." },
        { week: 5, source: "Day022 교재1", ko: "저희가 귀사의 서비스료를 감당하기 힘들 것 같습니다.", en: "I’m afraid we can’t afford your fees." },
        { week: 5, source: "Day022 교재2", ko: "폭스바겐 비틀 갖는 게 평생소원이었어. 이제 한 대 살 수 있을 줄 알았는데, 보니까 내가 감당하기 힘들 것 같아.", en: "I’ve wanted a Volkswagen Beetle my entire life. I thought I could get one now, but it looks like it’s more than I can afford." },
        { week: 5, source: "Day022 교재2", ko: "우선 돈을 모으고 몇 년 있다가 한 대 사. 아니면 꼭 갖고 싶으면 할부로 해. 너의 드림카잖아!", en: "Start saving and buy one in a few years. Or if you really want it, pay for it in installments. It’s your dream car!" },
        { week: 5, source: "Day022 교재2", ko: "매달 옷 사는 데 돈을 그렇게나 많이 쓰다니!", en: "I can't believe how much money you spend on clothes every month!" },
        { week: 5, source: "Day022 교재2", ko: "응, 나도 무리하는 거야. 빚이 산더미야.", en: "Yeah, I can’t really afford it. I’m deeply in debt." },
        { week: 5, source: "Day022 교재3", ko: "유니클로는 일본 어디에서나 볼 수 있으며 캐시미어 점퍼, 버튼다운셔츠, 경량 다운재킷과 같은 누구나 살수 있는 저렴한 기본 패션 아이템으로 전 세계적으로도 성공을 거두었습니다. 호주 매장은 2014년 4월멜버른에서 처음 오픈했으며 빠른 확장세를 보이면서 지금은 호주 전역에 걸쳐 16개의 매장을 가지고 있습니다.", en: "Uniqlo is ubiquitous in Japan and has found success across the globe with its range of basic fashion items anyone can afford, like cashmere jumpers, button-down shirts and lightweight down jackets. The chain opened its first Australian store in Melbourne in April 2014 and has expanded rapidly to now have 16 stores across all mainland states." },
        { week: 5, source: "Day022 교재4", ko: "네가 우리 딸 좀 맡아 줘야 할 것 같아.", en: "I think you could take her on." },
        { week: 5, source: "Day022 교재4", ko: "나 무지 비싸거든.", en: "You can’t afford me." },
        { week: 5, source: "Day022 교재4", ko: "점심시간은 꽉 채워서 한 시간이죠?", en: "Are you taking a full hour for lunch?" },
        { week: 5, source: "Day022 교재4", ko: "아니요, 바빠서 그렇게 오랜 시간 점심을 먹을 형편이 안 됩니다.", en: "No, I can’t afford to take that long." },
        { week: 5, source: "Day022 대표", ko: "저한테는 좀 부담스러운 금액이었어요.", en: "It was something I could barely afford." },
        { week: 5, source: "Day023 교재1", ko: "전부 제가 생각하고 있는 예산 밖이군요. 이십만 원 미만은 없을까요?", en: "This is all out of my price range. Don’t you have anything under 200,000 won?" },
        { week: 5, source: "Day023 교재1", ko: "제일 저렴한 것도 제 예산 밖이더라고요.", en: "Even the cheapest one was out of my price range." },
        { week: 5, source: "Day023 교재1", ko: "추천해 주신 나무 테이블이 제 예산을 훨씬 초과하네요.", en: "I’m afraid the wooden table you recommended is way out of my price range." },
        { week: 5, source: "Day023 교재1", ko: "제철이 아닌 과일이나 채소는 늘 너무 비싸요.", en: "Out-of-season fruit and vegetables are always out of my price range." },
        { week: 5, source: "Day023 교재1", ko: "우리 아파트 근처에 있는 쉐보레 매장에 가 봤는데, 내가 생각하는 가격대의 차는 없었어요.", en: "I checked out the Chevrolet dealership near my apartment, but they didn’t have anything in my price range." },
        { week: 5, source: "Day023 교재2", ko: "이 키보드에 관심 있는데요, 삼십만 원은 조금 비싸네요. 혹시 조금 깎아 주실 수 있는지요?", en: "I’m interested in this keyboard, but 300,000 won is a bit out of my price range. Could you go any lower?" },
        { week: 5, source: "Day023 교재2", ko: "어느 정도 생각하셨는데요?", en: "How much lower were you thinking?" },
        { week: 5, source: "Day023 교재2", ko: "저희 제품들은 모두 특별히 덴마크에서 수입해요. 이건 천만 원이에요.", en: "All of our selections are specially imported from Denmark. This one is 10 million won." },
        { week: 5, source: "Day023 교재2", ko: "아. 제 예산보다 훨씬 비싸군요. 좀 더 저렴한 건 없나요?", en: "Oh. That’s way out of my price range. Do you have anything cheaper?" },
        { week: 5, source: "Day023 교재2", ko: "매물로 나온 것을 보기 전에, 우선 생각하고 있는 금액대를 물어봐도 될까요?", en: "Before we get started looking at what’s available, can I ask your price range?" },
        { week: 5, source: "Day023 교재2", ko: "삼억 원 이상은 쓰고 싶지 않습니다.", en: "We wouldn’t want to spend more than 300 million won." },
        { week: 5, source: "Day023 교재3", ko: "(견적을 받아 본 고객이 인테리어 업자에게 보내는 이메일)\n견적서 감사드립니다. 귀사에서 제안 주신 내용이 저희 예산을 조금 초과합니다. (공사 비용을) 추가로 10% 깎아 주실 여지가 있을까요? 이해해 주시면 감사하겠습니다.", en: "Thank you for your quote. What you’re offering is a little out of our price range. Is there any way you can come down another 10%? I would appreciate your understanding." },
        { week: 5, source: "Day023 교재4", ko: "파리는 차도 너무 많고 식당도 너무 비싸.", en: "Paris is full of traffic and overpriced restaurants." },
        { week: 5, source: "Day023 교재4", ko: "강남에서는 커피가 너무 비싸다.", en: "Coffee is overpriced in Gangnam." },
        { week: 5, source: "Day023 교재4", ko: "광고 대행업체는 너무 비싸.", en: "Agencies are overpriced." },
        { week: 5, source: "Day023 교재4", ko: "호텔 식당은 항상 너무 비싸.", en: "Hotel restaurants are (always) overpriced." },
        { week: 5, source: "Day023 대표", ko: "제가 생각했던 것보다 비싸네요.", en: "This is all out of my price range." },
        { week: 5, source: "Day024 교재1", ko: "소파가 일 년밖에 안 됐는데 너덜너덜하네. 싼 게 비지떡이지 뭐.", en: "The couch is falling apart after only a year. We got what we paid for." },
        { week: 5, source: "Day024 교재1", ko: "4천 원도 안 되니 양질의 햄버거는 기대 안 해. 그래도 먹을 만은 해. 딱 그 가격인 듯.", en: "I don’t expect a quality fast food hamburger for less than 4,000 won, so it’s okay. I get what I pay for." },
        { week: 5, source: "Day024 교재1", ko: "왠지 너무 싸다 싶었어요. 싼 게 비지떡이죠.", en: "I should have known it was too good to be true. You get what you pay for." },
        { week: 5, source: "Day024 교재1", ko: "싼 게 비지떡이라는 점 꼭 기억하렴.", en: "Just keep in mind, you get what you pay for." },
        { week: 5, source: "Day024 교재1", ko: "(고가의 외제차 주인이 하는 말) 일억 주고 산 게 이 모양이네.", en: "This is what I get for 100 million won." },
        { week: 5, source: "Day024 교재2", ko: "나 이 헤어드라이어 동네 시장에서 샀는데 싸게 잘 샀다고 생각했거든. 근데 한 번 사용하고 고장나 버렸지 뭐야.", en: "I bought this hair dryer at a local market and I thought I got a great deal. But actually, it broke the first time I used it." },
        { week: 5, source: "Day024 교재2", ko: "싼 게 다 그렇지 뭐. 좋은 걸 원하면 다른 데 가 봐야지.", en: "Well, you get what you pay for. If you want something good, you need to go somewhere else." },
        { week: 5, source: "Day024 교재2", ko: "십만 원 버렸네.", en: "What a waste of 100,000 won!" },
        { week: 5, source: "Day024 교재2", ko: "왠지 너무 싸다고 했어. 싼 게 비지떡이지 뭐.", en: "I knew it was too good to be true. You get what you pay for, I guess." },
        { week: 5, source: "Day024 교재2", ko: "이 오븐 오만 원에 샀는데 한 달 만에 고장 났지 뭐야.", en: "I got this oven for just 50,000 won, but it broke after just a month." },
        { week: 5, source: "Day024 교재2", ko: "그럼 뭘 기대한 거니? 싼 게 비지떡이지.", en: "Well, what were you expecting? You get what you pay for." },
        { week: 5, source: "Day024 교재3", ko: "(허먼 밀러 의자 광고)\n경쟁사 제품과 비교하면 저희 의자가 최고 50%는 더 비쌉니다. 하지만 싼 게 비지떡이라는 점을 꼭 기억해 주세요. 저희 의자는 수리하지 않고 십 년까지 쓸 수 있는 의자입니다", en: "If you compare our prices to our competitors’, it is true that our chairs are up to 50% more expensive. Please keep in mind, you get what you pay for. Our chairs are guaranteed to last up to 10 years without needing repairs." },
        { week: 5, source: "Day024 교재4", ko: "쉐라톤 호텔에 묵을 거면 1일 패키지를 끊어야 해. 풀장 이용이 가능하고 라운지에서 음식과 음료를 무제한으로 즐길 수 있거든. 가성비로 치면 최고지!", en: "If you stay at the Sheraton, you gotta go with the all-day package. It comes with pool access and unlimited food and drinks at the lounge. It definitely gives you the best bang for your buck." },
        { week: 5, source: "Day024 교재4", ko: "이 청소기를 구매하실 것을 추천하는데요, 가성비가 가장 좋기 때문입니다.", en: "I recommend you buy this vacuum cleaner because it is the best bang for the buck." },
        { week: 5, source: "Day024 교재4", ko: "아이폰이 부담되시면, 이 삼성폰을 추천해 드립니다. 이 모델이 가성비가 가장 좋을 겁니다.", en: "If you can’t afford an iPhone, I’d recommend this Samsung. This model will give you the best bang for the buck." },
        { week: 5, source: "Day024 대표", ko: "싼 게 다 그렇지 뭐.", en: "You get what you pay for." },
        { week: 5, source: "Day025 교재1", ko: "마음에 들었다니 다행이네요.", en: "I’m glad you liked it." },
        { week: 5, source: "Day025 교재1", ko: "(파티에서 친구에게) 재미있다니 다행이네.", en: "I’m glad you are enjoying it." },
        { week: 5, source: "Day025 교재1", ko: "오늘 아침 발표를 잘했다니 다행입니다.", en: "I’m glad your presentation went well this morning." },
        { week: 5, source: "Day025 교재1", ko: "(늦게까지 술을 마시는 상황) 내일 일찍 안 일어나도 돼서 얼마나 다행인지.", en: "I’m glad I don’t have to wake up early tomorrow." },
        { week: 5, source: "Day025 교재1", ko: "제 말에 공감해 줘서 다행이네요.", en: "I’m glad you can relate." },
        { week: 5, source: "Day025 교재2", ko: "이 과자 어디서 샀어요? 너무 맛있어요!", en: "Where did you get these cookies? They’re great!" },
        { week: 5, source: "Day025 교재2", ko: "삼촌이 한 통 보내주셨는데 그 과자 회사에서 일하세요. 좋아하시니 다행입니다. 저희는 맛이 질려서요.", en: "We got a whole carton from my uncle, who works for the company. I’m glad you like them. We’re kind of sick of the taste." },
        { week: 5, source: "Day025 교재2", ko: "늦어서 미안. 일을 최대한 빨리 마치고 왔어.", en: "Sorry I’m late. I finished my work as fast as I could." },
        { week: 5, source: "Day025 교재2", ko: "못 올 줄 알았더니 와서 다행이다! 방금 시켰어. 앉아!", en: "I’m glad you could make it! We just ordered. Take a seat!" },
        { week: 5, source: "Day025 교재2", ko: "남자 친구랑 우리 감정에 대해 길게 이야기했고, 결국 화해했어.", en: "My boyfriend and I had a long conversation about our feelings, and we finally made up." },
        { week: 5, source: "Day025 교재2", ko: "이야기가 잘 됐다니 다행이다! 너희 둘은 너무 잘 어울려.", en: "I’m glad things worked out in the end! You two are great together." },
        { week: 5, source: "Day025 교재3", ko: "새 사무실 의자를 알아보러 갔더니 허먼 밀러를 추천해 주었다. 온라인에서 허먼 밀러 의자들을 봤을 때는 예쁘긴 했지만 이백사십만 원이나 하는 게 이해가 안 됐다. 그래도 그냥 사 버렸고, 잘했다 싶다. 정말 너무 편하다.", en: "I was in the market for a new office chair, and Herman Miller was recommended to me. When I saw a good-looking chair of theirs online, I didn’t see how it could possibly be worth 2.4 million won. I went ahead and bought it anyway, and I’m glad I did. I can’t believe how comfy it is." },
        { week: 5, source: "Day025 교재4", ko: "이건 어디서 샀나요?", en: "Where did you get these?" },
        { week: 5, source: "Day025 교재4", ko: "좋아하시니 다행이네요. 있잖아요, 아침마다 이걸 가지고 오겠습니다.", en: "I’m glad you like them. You know what? I’ll start bringing these to you every morning." },
        { week: 5, source: "Day025 교재4", ko: "시즌 3도 나온다니 너무 좋아.", en: "I am happy that they are going to come out with a third season." },
        { week: 5, source: "Day025 교재4", ko: "또 승진에서 누락되어서 실망입니다.", en: "I am disappointed that I have been passed over for a promotion once again." },
        { week: 5, source: "Day025 대표", ko: "베이비시터 구했다니 다행입니다", en: "I’m glad you found a babysitter." }
    ];

    // 영어회화 난이도 분리
    const convEasy = rawConvData.filter(item => item.source.includes('대표') || item.source.includes('교재1'));
    const convHard = rawConvData.filter(item => !(item.source.includes('대표') || item.source.includes('교재1')));

    // 퀴즈 진행 상태 변수
    let currentQuestions = [];
    let currentIndex = 0;
    let isPhrasalMode = false;
    let starredQuestions = []; 

    function shuffleArray(array) {
        let shuffled = [...array];
        for (let i = shuffled.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
        }
        return shuffled;
    }

    // 선택된 주차에 맞게 필터링
    function filterByWeek(dataArray) {
        if (currentWeekFilter === 'all') {
            return dataArray;
        }
        return dataArray.filter(item => item.week === currentWeekFilter);
    }

    function startQuiz(mode) {
        let sourceArray = [];
        let titleMode = "";

        if (mode === 'phrasal-easy') { 
            sourceArray = phrasalEasy; isPhrasalMode = true; 
            titleMode = "🟢 구동사 순한맛 퀴즈"; 
        }
        else if (mode === 'phrasal-hard') { 
            sourceArray = phrasalHard; isPhrasalMode = true; 
            titleMode = "🔴 구동사 매운맛 퀴즈"; 
        }
        else if (mode === 'conv-easy') { 
            sourceArray = convEasy; isPhrasalMode = false; 
            titleMode = "💬 영어회화 순한맛 퀴즈"; 
        }
        else if (mode === 'conv-hard') { 
            sourceArray = convHard; isPhrasalMode = false; 
            titleMode = "🔥 영어회화 매운맛 퀴즈"; 
        }

        const filteredData = filterByWeek(sourceArray);

        if (filteredData.length === 0) {
            alert(`선택하신 주차(${currentWeekFilter === 'all' ? '누적' : 'Week ' + currentWeekFilter})에 해당하는 데이터가 아직 없습니다.`);
            return;
        }

        document.getElementById('mode-selection').classList.add('hidden');
        document.getElementById('quiz-area').classList.remove('hidden');
        
        let weekText = currentWeekFilter === 'all' ? " (5~8주차 누적)" : ` (Week ${currentWeekFilter})`;
        document.getElementById('main-title').innerText = titleMode + weekText; 
        
        starredQuestions = []; 
        // 7문제만 추출 (데이터가 7개 미만이면 전체 추출)
        const qCount = Math.min(filteredData.length, 7);
        currentQuestions = shuffleArray(filteredData).slice(0, qCount);
        currentIndex = 0;
        
        loadQuestion();
    }

    function loadQuestion() {
        document.getElementById('answer-section').classList.add('hidden');
        document.getElementById('btn-next').classList.add('hidden');
        document.getElementById('btn-finish').classList.add('hidden');
        document.getElementById('meaning-info').classList.add('hidden');
        
        const koBox = document.getElementById('ko-box');
        koBox.style.cursor = 'pointer';
        koBox.style.pointerEvents = 'auto';

        const q = currentQuestions[currentIndex];
        document.getElementById('question-counter').innerText = `문제 ${currentIndex + 1} / ${currentQuestions.length}`;
        document.getElementById('ko-text').innerText = q.ko;
        document.getElementById('en-text').innerText = q.en;
        document.getElementById('source-info').innerText = `출처: ${q.source}`;
        
        if(isPhrasalMode && q.meaning) {
            document.getElementById('meaning-info').innerText = q.meaning;
        }

        const starBtn = document.getElementById('btn-star');
        if (starredQuestions.includes(q)) {
            starBtn.classList.add('active');
            starBtn.innerText = "⭐ 어려워요 (저장됨)";
        } else {
            starBtn.classList.remove('active');
            starBtn.innerText = "⭐ 어려워요";
        }
    }

    function showAnswer() {
        const koBox = document.getElementById('ko-box');
        koBox.style.cursor = 'default';
        koBox.style.pointerEvents = 'none';

        document.getElementById('answer-section').classList.remove('hidden');
        
        if(isPhrasalMode && currentQuestions[currentIndex].meaning) {
            document.getElementById('meaning-info').classList.remove('hidden');
        }
        
        if (currentIndex < currentQuestions.length - 1) {
            document.getElementById('btn-next').classList.remove('hidden');
        } else {
            document.getElementById('btn-finish').classList.remove('hidden');
        }
    }

    function toggleStar() {
        const q = currentQuestions[currentIndex];
        const starBtn = document.getElementById('btn-star');
        const index = starredQuestions.indexOf(q);
        
        if (index > -1) {
            starredQuestions.splice(index, 1);
            starBtn.classList.remove('active');
            starBtn.innerText = "⭐ 어려워요";
        } else {
            starredQuestions.push(q);
            starBtn.classList.add('active');
            starBtn.innerText = "⭐ 어려워요 (저장됨)";
        }
    }

    function playTTS() {
        const textToSpeak = currentQuestions[currentIndex].en;
        if ('speechSynthesis' in window) {
            window.speechSynthesis.cancel();
            const utterance = new SpeechSynthesisUtterance(textToSpeak);
            utterance.lang = 'en-US';
            utterance.rate = 0.9; 
            window.speechSynthesis.speak(utterance);
        } else {
            alert('이 브라우저에서는 음성 듣기 기능을 지원하지 않습니다.');
        }
    }

    function nextQuestion() {
        currentIndex++;
        loadQuestion();
    }

    function showReview() {
        document.getElementById('quiz-area').classList.add('hidden');
        document.getElementById('review-area').classList.remove('hidden');
        document.getElementById('main-title').innerText = "결과 및 오답 노트";

        const reviewList = document.getElementById('review-list');
        reviewList.innerHTML = '';

        if (starredQuestions.length === 0) {
            reviewList.innerHTML = `<div class="review-empty">🎉 어려운 문장이 없습니다! 완벽해요! 🎉</div>`;
        } else {
            starredQuestions.forEach((q, idx) => {
                let meaningHtml = (isPhrasalMode && q.meaning) ? `<div style="font-size: 13px; color: #b45309; background: #fef3c7; padding: 4px 8px; border-radius: 4px; display: inline-block; margin-bottom: 5px;">${q.meaning}</div>` : '';
                
                reviewList.innerHTML += `
                    <div class="review-card">
                        <div style="font-size: 12px; color: #94a3b8; margin-bottom: 5px;">${idx + 1}. 출처: ${q.source}</div>
                        ${meaningHtml}
                        <div class="review-ko">${q.ko}</div>
                        <div class="review-en">${q.en}</div>
                    </div>
                `;
            });
        }
    }

    function resetToHome() {
        document.getElementById('review-area').classList.add('hidden');
        document.getElementById('mode-selection').classList.remove('hidden');
        document.getElementById('main-title').innerText = "🚀 스피드 영어 퀴즈";
    }
</script>

</body>
</html>
