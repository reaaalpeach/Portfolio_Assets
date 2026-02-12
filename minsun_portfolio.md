# [Project] NCT ZONE - Content & System Client Develop
> **NCT 멤버들과 함께하는 시네마틱 어드벤처 게임의 핵심 시스템 개발 및 라이브 서비스 개발/유지 보수**

---

## 📌 Project Overview
- **개발 기간:** 2022.11 ~ 2022.02
- **기술 스택:** Unity 3D, C#, UGUI
- **담당 역할:** 클라이언트 컨텐츠 로직 구현 (스테이지, 시스템, 미니게임, 덱, 빙고게임)

---

## 🎮 Key Implementation

### 1️⃣ 스테이지 & 챕터 시스템 (Stage & Chapter)
다양한 게임 모드(Normal, Hard, Event)에 대응하기 위해 확장성 있는 데이터 구조를 설계하고 관리 시스템을 구현했습니다.
- **주요 구현:** 
    - 챕터 간 이동 및 해금 조건 체크 시스템 구현
    - 모드별 데이터 격리 구조: Enum 타입을 활용한 스테이지 카테고리 분류 및 모드별 독립적 데이터 테이블 관리로 데이터 혼선 방지.
    - 이벤트 스테이지 제어: 기간 한정 컨텐츠를 위해 서버 시간과 연동된 활성화/비활성화 스케줄링 로직 구현.
    - 추상화 기반 설계: 각 모드가 동일한 인터페이스를 공유하되, 보상 산정 및 난이도 계산 로직은 각 모드에 맞게 동작하도록 설계.

<p align="left">
  <img src="https://github.com/user-attachments/assets/6006a790-1e9b-4d6b-b1ee-1a1308b93348" width="20%" alt="Stage System Screenshot1">
  <img src="https://github.com/user-attachments/assets/71e51b5b-0d2b-477a-abeb-23ee61b53412" width="20%" alt="Worldmap">
  <img src="https://github.com/user-attachments/assets/484f0407-ebd6-4300-84f3-f0b2626e0b33" width="20%" alt="Stage Enter Popup">
</p>
 
- **Troubleshooting:** 
- 스테이지 전환 시의 메모리 부하를 줄이기 위해 어드레서블(Addressables)을 활용한 리소스 로드 최적화
- 기존 시스템에서 하드 모드와 이벤트 스테이지가 추가됨에 따라 데이터 구조가 복잡해지는 문제가 발생.
이를 해결하기 위해 각 모드를 Data Layer에서 분리하고, partial 키워드를 통해 class를 나누고 데이터 오염 방지와 유지보수 편의성을 동시에 확보.

### 2️⃣ 덱 저장 시스템 (Deck Management)
유저가 스테이지 공략을 위해 설정한 최적의 카드 조합을 로컬 및 서버에 저장하고 불러오는 기능을 구현했습니다.
- **주요 구현:**
    - 다중 덱 슬롯 관리 로직
    - 보스별 속성 상성과 카드의 상성에 따른 빠른 편성 기능 추가 

<p align="left">
  <img src="https://github.com/user-attachments/assets/f0d3182c-3baf-4f0c-ac87-f5ed9096adc7" width="20%" alt="Deck Editing1">
  <img src="https://github.com/user-attachments/assets/0c3e2702-a99c-4fd0-af3a-9c289ea0b692" width="20%" alt="Deck Editing2">
</p>

- **Troubleshooting:** 기존 시스템에서 타입별로 덱을 구성하게됨에 따라 데이터 구조가 복잡해지는 문제가 발생.
이를 해결하기 위해 상속을 통해 공통 로직은 재사용하되 타입별 특수 로직은 개별적으로 처리하도록 구현하여 데이터 오염 방지 및 유지 보수 편의성을 동시에 확보.

### 3️⃣ 빙고 이벤트 시스템 (Bingo System)
미션 수행과 재화 소모를 결합하여 유저의 리텐션을 유도하는 이벤트 시스템을 개발했습니다.
- **주요 구현:**
    - **이원화 도장 시스템:** 미션 보상(일반 도장)과 유료 재화(스페셜 도장) 사용 로직 구현
    - **빙고 판정 알고리즘:** 5x5 그리드의 가로, 세로, 대각선 완성 여부를 실시간 검출
    - **최종 보상 연동:** 올빙고 달성 시 '미공개 사진' 뷰어 및 해금 연출 구현

<p align="left">
  <img src="https://github.com/user-attachments/assets/b81fe47f-739d-4c25-977c-e8ad123d71a8" width="20%" alt="Bingo">
  <img src="https://github.com/user-attachments/assets/6e088cdf-e081-4584-b003-817c277f46e8" width="20%" alt="Bingo Line Clear">
  <img src="https://github.com/user-attachments/assets/e3c224e0-ba80-4e0d-968b-149e660786eb" width="20%" alt="Bingo Mission">
</p>

### 3️⃣ 미니게임 2종 (Mini Games)
게임 내 체류 시간을 높이기 위한 캐주얼 미니게임의 핵심 메카닉을 개발했습니다.

#### 🏎️ 레이싱 미니게임
- 물리 기반의 차량 컨트롤러 구현
- 무한 맵 생성을 위한 오브젝트 풀링(Object Pooling) 적용

<p align="left">
  <img src="https://github.com/user-attachments/assets/60bed8a2-d169-4c27-b874-ecfac5a0cd05" width="20%" alt="Racing Main">
  <img src="https://github.com/user-attachments/assets/62c30b50-00df-4cc7-8a7e-3ad5d9c26121" width="20%" alt="Racing Playing">
</p>

- **Troubleshooting:** 다양한 아이템 연출이 겹칠 때 프레임 드랍이 발생하는 문제를 방지하기 위해, 이펙트 오브젝트에도 오브젝트 풀링을 적용하여 안정적인 성능을 유지.

#### 🍉 수박게임 (Merge Mechanic)
- 오브젝트 풀링을 이용한 게임 최적화
- 원형 물리 충돌 판정을 이용한 오브젝트 합성 로직
- 상단 투하 위치 가이드 및 스코어 시스템

<p align="left">
  <img src="https://github.com/user-attachments/assets/8d2f26f2-0c23-4760-affc-bdfa4dbefb5c" width="20%" alt="Watermelon Main">
  <img src="https://github.com/user-attachments/assets/0bcb49e5-613d-43d8-826c-598bda604a12" width="20%" alt="Watermelon Playing">
  <img src="https://github.com/user-attachments/assets/a8f720b0-78f1-48f0-a938-a6ddbb768732" width="20%" alt="Watermelon Select Item">
</p>

#### 미니게임 공통 적용 사항
- 아이템 시스템 : 각기 다른 효과(턴 추가, 통흔들기, 지정해서 없애기 등)를 가진 아이템을 고유 트리거 시스템을 통해 사용 즉시 연동되는 특수 효과 및 로직을 구현하고, 게임의 템포를 조절하는 다양한 변수 창출.
- 랭킹 시스템 : 전체 유저 대상의 '글로벌 랭킹'과 소셜 연동 정보를 활용한 '친구 랭킹' 데이터 분리 및 UI 대응.

<p align="left">
  <img src="https://github.com/user-attachments/assets/8b2d59ba-cf36-4f75-9f5d-71909796d7fa" width="20%" alt="MiniGame Ranking System">
</p>

- **Troubleshooting:** 다양한 아이템 연출이 겹칠 때 프레임 드랍이 발생하는 문제를 방지하기 위해, 이펙트 오브젝트에도 오브젝트 풀링을 적용하여 안정적인 성능을 유지.
---

## 💻 Code Snippets

### [Stage & Chapter System]

<details>
<summary><b>1️⃣ 모드별 데이터 구분을 위한 구조</b></summary>
    public enum CHAPTER_MODE
    {
        MODE_NORMAL,
        MODE_HARD,
        EVENT
    }
    
    public List<StageList> stage_list = new();              // 챕터의 모든 스테이지 리스트
    public List<ChapterList> chapterList = new();
    
    public partial class KwangyaManager : SingletonMono<KwangyaManager>
    {
        public void SetStageList(List<StageList> list) // 서버 스테이지 정보 셋팅
        {
            if (list != null)
            {
                stage_list?.Clear();

                list.ForEach(info =>
                {
                    if (GetMirrorStageData(info.gdid).mirrorstg_enable == (int)COMMON_AVAILABILLITY.BOOL_ENABLE)
                        stage_list.Add(info);
                    else
                        CDebug.Log($"Kwnagya SetStageList {info.gdid}", CDebugTag.KWANGYA);
                });
            }
        }
    
        public MirrorStageData GetMirrorStageData(int stage_id) // 스테이지에 따른 테이블 정보 가져오기
        {
            if (stage_id < 0)
                return null;

            return CMirrorDataManager.Instance.GetMirrorStageData(stage_id);
        }
    
        public StageList GetStage(int stage_id)
        {
            if (GetStageListByKwangyaType().Count <= 0)
                return null;

            StageList stage = new();
            GetStageListByKwangyaType().ForEach(info =>
            {
                if (info.gdid == stage_id)
                {
                    stage = info;
                }
            });

            return stage;
        }
    
        public List<StageList> GetStageListByKwangyaType() // 
        {
            if (kwangyaType == KWANGYA_TYPE.KWANGYA)
                return stage_list;
            else
                return evt_stage_list;
        }
    }
    
</details>    


### [Deck System]

<details>
<summary><b>1️⃣ 덱 데이터 구조 및 저장 로직 (클릭하여 펼치기)</b></summary>
   
        public class CardDeckEditing : CPopupUI<CardDeckEditing.Setting, CardDeckEditing.Result>
        {
            protected List<CardList> cardPacketList = new List<CardList>();
            protected List<int> deckPacketList = new List<int>();
            protected List<CardList> curDeckCardList = new List<CardList>(); // 현재 열려있는 덱에 있는 카드리스트
            protected Dictionary<int, List<CardList>> deckCardDic = new Dictionary<int, List<CardList>>(); // 덱이 여러개일 경우 덱마다 카드리스트 관리

            protected int curDeckIndex = 0; // 덱이 여러개일 경우 해당 덱의 인덱스

            protected virtual void SetDeckList(DeckList deckList, List<DeckList> decksList = null)
            {
                List<DeckList> decks = new List<DeckList>();
                if (deckList != null) // 덱 1개일 경우
                {
                    if(deckList.character0 > 0)
                        decks.Add(deckList);
                }
                else
                    decks = decksList != null ? decksList : null;

                isServerDeckEmpty = decks == null || decks != null && decks.Count <= 0;

                if (isServerDeckEmpty)
                    SetTempDeckInfo();
                else
                {
                    for (int i = 0; i < decks.Count; i++)
                    {
                        var deck = decks[i];
                        SetDeckData(0, deck.character0, i);
                        SetDeckData(1, deck.character1, i);
                        SetDeckData(2, deck.character2, i);
                        SetDeckData(3, deck.character3, i);
                        SetDeckData(4, deck.character4, i);
                        SetDeckData(5, deck.character5, i);
                        SetDeckData(6, deck.character6, i);
                        SetDeckData(7, deck.character7, i);
                    }
                }
            }

            protected void SetDeckData(int index, int cardId, int deckIndex = 0, bool isInit = true)
            {
                CardList cardData = null;
                bool isSameWeakPoint = false;
                if (cardId > 0)
                {
                    cardData = cardPacketList.Find(c => c.gdid == cardId);
                    isSameWeakPoint = CheckWeakPoint(cardData.GetDPZTYPE(), deckIndex);
                }

                deck.SetData(index, cardData, this, OnClickCardEvent, isSameWeakPoint, cardDeckUseType, deckIndex);
                SetDeckCardDic(cardData, deckIndex);

                if(isInit)
                    deckPacketList.Add(cardId);
            }

            public virtual void OnSave()
            {
                if (IsBtnDisable)
                    return;

                var popup = popupService.NoticeAlert("Mirror_deck_full_pop_desc", PopupAlert.BUTTON_TYPE.BTN_TWO);

                SingleAssignmentDisposable dispose = new SingleAssignmentDisposable();
                dispose.Disposable = popup.ShowAsObservable()
                .Do(result =>
                {
                    if (result.IsSucess)
                    {
                        if (IsModified())
                        {
                            var saveData = GetServerSaveData();
                            ServerDeckSave(saveData);
                        }
                        else
                            OnClickClose();
                    }
                    dispose.Dispose();
                }).Subscribe().AddTo(this);
            }

            protected Dictionary<int, List<int>> GetServerSaveData()
            {
                int idCnt = 8;
                Dictionary<int, List<int>> deckIdDic = new Dictionary<int, List<int>>();
                for (int i = 0; i < deckCnt; i++)
                {
                    List<int> deckIdList = new List<int>();
                    if (deckCardDic.ContainsKey(i))
                    {
                        for (int k = 0; k < idCnt; k++)
                        {
                            var tempDeck = deck.GetDeckByIndex(k, i);
                            deckIdList.Add(tempDeck.Id);
                        }
                    }
                    else
                    {
                        for (int k = 0; k < idCnt; ++i)
                        {
                            deckIdList.Add(0);
                        }
                    }

                    deckIdDic.Add(i, deckIdList);
                }

                // 덱 최대갯수보다 현재 덱갯수가 작을 때, 패킷에 보낼 빈 덱 추가
                if (deckIdDic.Count < deckCntMax)
                {
                    int emptyDeck = deckIdDic.Count;
                    for (int i = emptyDeck; i < deckCntMax; i++)
                    {
                        deckIdDic.Add(i, null);
                    }
                }

                return deckIdDic;   
            }

            protected virtual void ServerDeckSave(Dictionary<int, List<int>> deckIdList) // 타입별로 덱 
            {

            }
        }

</details>

<details> 
<summary><b>2️⃣ 세부 덱 정보 (클릭하여 펼치기)</b></summary>

            public void SetData(CardList cardInfo, CardDeckEditing deckEditing, CardDeckEditing.EditingType editingType,
                    int index, bool isSameWeakPoint, CardDeckUseType useType, int deckIndex)
            {
                this.index = index;
                this.deckEditing = deckEditing;
                this.cardInfo = cardInfo;
                this.editingType = editingType;
                this.isSameWeakPoint = isSameWeakPoint;
                this.useType = useType;
                this.deckIndex = deckIndex;   

                inRectCard = null;

                if(infoRootGo != null)
                {
                    if (editingType == CardDeckEditing.EditingType.Deck)
                    {
                        IsInfoGo = Id > 0;
                        IsCardInfoOn = Id > 0;  
                        SetCoverBlack(false);
                    }

                    if (!IsActive)
                        IsActive = true;

                    UpdateUI();
                }
            }

</details>
    
### [Bingo Game]

<details>
<summary><b>1️⃣ 슬롯 데이터 </b></summary>
    
    public class ObjBingoSlot : MonoBehaviour
    {
        private BingoSlotData slotData = null;
        private PageBingoEvent PageBingoEvent;
    
        public void Init(BingoSlotData data, BINGO_SLOT_STATE _state, int _slotIdx, PageBingoEvent _pageBingoEvent) // 개별 빙고데이터 셋팅
        {
            PageBingoEvent = _pageBingoEvent;   
            slotData = data;
            state = _state;
            index = _slotIdx;

            rootObj.SetActive(state == BINGO_SLOT_STATE.CLOSED);
            lockObj.SetActive(data.slotType == BING0_SLOT_TYPE.BINGO_SLOT_LOCK);
            slotNumText.text = index.ToString();  
        }
    
        public void OpenSlot()
        {
            state = BINGO_SLOT_STATE.OPEN;

            var popupBingoCommonStamp = CCoreServices.GetInstance().GetService<CPopupService>().GetPopup<PopupBingoCommonStamp>();
            if (popupBingoCommonStamp != null)
                popupBingoCommonStamp.Close();

            PlayEffSound();
            openAnim.Play();

            StartCoroutine(PageBingoEvent.CompleteLine(index, openAnim));
        }
    }
    
    public class PageBingoEvent : PagePopup
    {
        private BingoInfo bingoEventData; // 서버 데이터
        private List<BingoList> bingoStepList = new List<BingoList>(); // 테이블 데이터
    
        private void Init()
        {
            bingoEventData = APIHelper.BingoService.BingoInfo;
            bingoStepList = APIHelper.BingoService.BingoStepList;
            curEventTbData = CEventDataManager.Instance.GetBingoEventData(bingoEventData.gdid);

            SetCurBingoStep(APIHelper.BingoService.GetLastOpenBingoData());
            SetLineRwdDic();
            SetEventInfo();
            SetStampInfo();
            SetEventTimer();
            SetMissionRedDot(bingoEventData.mission_reddot);
        }
    
        public IEnumerator CompleteLine(int slotIdx, Animation anim)
        {
            yield return new WaitUntil(() => !anim.isPlaying);

            var clearDic = GetClearLineBySlotIdx(slotIdx);
            if (clearDic.Count < 1)
            {
                Utility.SetFxLayerDimmed(false);
                yield break;
            }

            foreach (var dic in clearDic)
            {
                var rwdIndex = dic.Key - 1;
                var slotList = dic.Value;
                for (int i = 0; i < slotList.Count; i++)
                {
                    var slot = slotList[i];

                    slot.PlayOpenAnim();

                    if (i < slotList.Count -1)
                        yield return new WaitForSeconds(delay.slot);
                    else
                        yield return new WaitForSeconds(delay.lineRwd);
                }

                CSoundControl.Instance?.EffectPlay(SOUND_ID.SFX_BINGO_LINE);
                objLineRwdList[rwdIndex].SetState(BINGO_RWD_STATE.RWD_OPEN);

                yield return new WaitForSeconds(delay.line);
            }

            if (CheckBingoAllClear())
            {
                imgBlur.enabled = false;
                bingoLineOBj.SetActive(false);
                SetDesc();

                yield return new WaitForSeconds(delay.openPopup);

                OpenPopupBingolear();
            }
            else
                Utility.SetFxLayerDimmed(false);
        }
    }

</details>
    
<details> <summary><b>1️⃣ 라인 완성 체크 및 연출 </b></summary>
    
    public class ObjBingoSlot : MonoBehaviour
    {
        public void OpenSlot()
        {
            state = BINGO_SLOT_STATE.OPEN;

            var popupBingoCommonStamp = CCoreServices.GetInstance().GetService<CPopupService>().GetPopup<PopupBingoCommonStamp>();
            if (popupBingoCommonStamp != null)
                popupBingoCommonStamp.Close();

            PlayEffSound();
            openAnim.Play();

            StartCoroutine(PageBingoEvent.CompleteLine(index, openAnim));
        }
    }
    
    public class PageBingoEvent : PagePopup
    {
        public IEnumerator CompleteLine(int slotIdx, Animation anim)
        {
            yield return new WaitUntil(() => !anim.isPlaying);

            var clearDic = GetClearLineBySlotIdx(slotIdx);
            if (clearDic.Count < 1)
            {
                Utility.SetFxLayerDimmed(false);
                yield break;
            }

            foreach (var dic in clearDic)
            {
                var rwdIndex = dic.Key - 1;
                var slotList = dic.Value;
                for (int i = 0; i < slotList.Count; i++)
                {
                    var slot = slotList[i];

                    slot.PlayOpenAnim();

                    if (i < slotList.Count -1)
                        yield return new WaitForSeconds(delay.slot);
                    else
                        yield return new WaitForSeconds(delay.lineRwd);
                }

                CSoundControl.Instance?.EffectPlay(SOUND_ID.SFX_BINGO_LINE);
                objLineRwdList[rwdIndex].SetState(BINGO_RWD_STATE.RWD_OPEN);

                yield return new WaitForSeconds(delay.line);
            }

            if (CheckBingoAllClear())
            {
                imgBlur.enabled = false;
                bingoLineOBj.SetActive(false);
                SetDesc();

                yield return new WaitForSeconds(delay.openPopup);

                OpenPopupBingolear();
            }
            else
                Utility.SetFxLayerDimmed(false);
        }
                                          
        private bool CheckBingoAllClear() // 빙고 전체 클리어 
        {
            bool isClear = true;
            for(int i = 0; i < curBingoData.slots.Count; i++)
            {
                var slot = curBingoData.slots[i];
                if (slot != (int)BINGO_SLOT_STATE.OPEN)
                {
                    isClear = false;
                    break;
                }
            }

            return isClear;
        }
    }
    
</details>

### [Mini Game]
#### 🏎️ 레이싱 미니게임
    
<details> <summary><b>1️⃣ 충돌 체크 </b></summary>
    
    public class MiniGameCharacterTrigger : MonoBehaviour
    {
        private MiniGameObjectPool gameObjectPool;
    
        protected void OnTriggerEnter(Collider c)
        {
            // 충돌이벤트 설정
            if (!MiniGameManager.Instance.isTriggerEnter)
                return;

            if (c.gameObject.layer == k_CoinsLayerIndex)
            {
                gameObjectPool = c.GetComponent<MiniGameObjectPool>();

                if (gameObjectPool == null)
                {
                    CDebug.Log($"[MINIGAME] OnTriggerEnter null {c.gameObject}");
                    return;
                }

                // 피버모드
                if (MiniGameManager.Instance.IsFeverMode)
                    OnTriggerFeverMode(c);
                else// 일반모드
                    OnTriggerNormalMode(c);
            }
        }
    
        private void OnTriggerNormalMode(Collider c) // 일반 모드에 따른 오브젝트 충돌 처리
        {
            // 아이템 획득 처리
            MiniGameManager.Instance.SetMiniGameItem(gameObjectPool.obj_id);

            switch (gameObjectPool.obj_type)
            {
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_HURDLE:
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_MONSTER:
                    // 중복 히트 방지
                    StartCoroutine(OnTriggerBoxColliderEnabled());
                    // 무적 모드
                    if (MiniGameManager.Instance.IsInvincibility == false)
                    {
                        SetHitObject(gameObjectPool.obj_type, c);
                    }
                    break;
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_COIN:
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_TIME:
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_BOOST:
                    MiniGameObjectPool.objectPool.Free(c.gameObject);
                    break;
            }
        }
    
        private void OnTriggerFeverMode(Collider c) // 피버모드 충돌 처리
        {
            // 아이템 획득 처리
            MiniGameManager.Instance.SetFeverModeMiniGameItem(gameObjectPool.obj_type);

            switch (gameObjectPool.obj_type)
            {
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_HURDLE:
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_MONSTER:
                    CSoundControl.Instance?.EffectPlay(SOUND_ID.SFX_MG_BUMP_03);
                    StartCoroutine(gameObjectPool.SetFeverMode());
                    break;

                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_COIN:
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_TIME:
                case MiniGameObjectPool.MINI_GAME_OBJ_TYPE.RACING_OBJ_BOOST:
                    MiniGameObjectPool.objectPool.Free(c.gameObject);
                    break;
            }
        }
    }
        
</details>
 
#### 🍉 수박게임
    
<details> <summary><b>1️⃣ 구슬  </b></summary>
    public partial class MiniGameWatermelon : MiniGameCommon
    {
        public enum WATERMELON_TYPE
        {
            NONE            = 0,
            BEAD_NORMAL     = 1,
            BEAD_STACKUP    = 2,
            BEAD_RAINBOW    = 3,
        }
    
        private void CreateObjectPool() // 구슬 오브젝트 풀 생성
        {
            if (WatermelonObj == null)
                WatermelonObj = CResourceManager.Instance.LoadObject(CPREFAB_KEY.minigame_watermlon_bead) as GameObject;

            if (WatermelonObj != null)
            {
                MiniGameWatermelonController bead = WatermelonObj.GetComponent<MiniGameWatermelonController>();

                if (bead != null)
                    bead.LoadBeadResource();

                // 구슬 오브젝트 풀링
                objectPool = new MiniGamePooler(WatermelonObj, MiniGamePoolerMax);
            }
        }
    
        public void CreateOBJ(bool isInit = false) / 구슬 생성
        {
            if (GameState == MiniGameState.GameEnd || isTurnEnd || isDeadLine)
                return;

            if (CheckBeadCount())
                return;

            nextBead = objectPool.Get(objPivot.transform.position, Quaternion.identity);

            if (nextBead != null)
            {
                nextBead.transform.SetParent(objPivot.transform, true);
                BeadController = nextBead.GetComponent<MiniGameWatermelonController>();
                var beadType = (WATERMELON_TYPE)BeadListData[bead_rate_value].bead_type;

                BeadController.SetBeadData(beadType, bead_rate_value, BeadListData[bead_rate_value].bead_id, avatarHolder.transform);

                if (isInit)
                {
                    SetNextBeadSprite();
                    UseStartItem();
                    IsBeadDrop = true;
                }

                PageMinigameWmhud.Instance.SetNextBead(); // 다음 구슬 셋팅
                GetMiniGamePlayer.PlayerAnimation.SetGripAnim(); // 캐릭터 애니메이션 셋팅
            }
        }
    }
    
</details>
    
<details> <summary><b>2️⃣ 구슬 드랍 </b></summary>    
    
    public class MiniGameWatermelonPlayer : MiniGamePlayerInput
    {
        private void ObjectDrop()
        {
            playerAnimation.PlayAnim("isDrop");
            MiniGameWatermelon.Instance.IsBeadDrop = false;

            if (mBeadController != null)
            {
                mBeadController.transform.SetParent(MiniGameWatermelon.Instance.watermelonMap.transform, true);
                mBeadController.ChangeBeadData(MiniGameWatermelon.Instance.map_id);

                MiniGameWatermelon.Instance.AddMap(mBeadController);
                MiniGameWatermelon.Instance.SetMyTurn();
            }

            lineRenderer.positionCount = 0; // 라인 비활성화

            if (nextBeadCo != null)
            {
                StopCoroutine(nextBeadCo);
                nextBeadCo = null;
            }

            nextBeadCo = StartCoroutine(MiniGameWatermelon.Instance.CreateNextOBJ());
            SetisPlayerHit(false);
        }
    }
    
</details>
    
<details> <summary><b>3️⃣ 충돌 처리 </b></summary>     
    
    private void OnHit(Collision2D collision)
    {
        if (collision.gameObject == null || gameObject.activeInHierarchy == false)
            return;

        if (isHit)
            return;
        else
        {
            // 바닥에 부딪혔을 때
            if(isTriggerEnter == false)
            {
                if (collision.gameObject.CompareTag("obj_resultcard"))
                {
                    isTriggerEnter = true;
                    ResetIsFly();
                    MiniGameWatermelon.Instance.SetPlayerMove(true);
                    return;
                }
            }
        }

        // 타겟 충돌
        if (collision.gameObject.TryGetComponent<MiniGameWatermelonController>(out var targetController))
        {
            switch (m_beadType)
            {
                // 구슬 노멀
                case MiniGameWatermelon.WATERMELON_TYPE.BEAD_NORMAL:
                    //같은 단계의 구슬
                    if (targetController.m_beadStep == m_beadStep)
                    {
                        if (targetController.m_beadType != MiniGameWatermelon.WATERMELON_TYPE.BEAD_RAINBOW)
                            SetHit(targetController);
                    }
                    else
                    {
                        //CheckFly();
                        CheckMoving();
                        // 다른 단계의 구슬(이동만 가능하게)
                        MiniGameWatermelon.Instance.SetPlayerMove(true);
                    }

                    break;
                // 안터지는 구슬
                case MiniGameWatermelon.WATERMELON_TYPE.BEAD_STACKUP:
                    isTriggerEnter = true;
                    //CheckFly();
                    CheckMoving();
                    MiniGameWatermelon.Instance.SetPlayerMove(true);
                    break;
                // 모든 종류의 TYPE_NORMALBEAD 구슬과 합쳐짐
                case MiniGameWatermelon.WATERMELON_TYPE.BEAD_RAINBOW:
                    // 안터지는 구슬 (무지개) 제외 모든 구슬
                    if (targetController.m_beadType != MiniGameWatermelon.WATERMELON_TYPE.BEAD_STACKUP && targetController.m_beadType != MiniGameWatermelon.WATERMELON_TYPE.BEAD_RAINBOW)
                    {
                        SetHit(targetController, true);
                    }
                    break;
            }
        }
    }
        
</details>
    
---

## 📈 Growth & Review
- **데이터 설계 능력 향상:** Normal/Hard/Event 등 복잡한 라이브 서비스 환경에서 데이터 간섭 없이 안정적으로 확장 가능한 시스템 설계 역량을 쌓았습니다.
- **최적화 및 UX 고려:** 대량의 랭킹 데이터 처리 및 오브젝트 풀링을 활용한 미니게임 구현을 통해 성능 최적화와 유저 피드백(연출)의 중요성을 체득했습니다.
- **협업 중심 개발:** 기획 의도에 유연하게 대응할 수 있도록 추상화와 인터페이스 중심의 코드를 작성하여 유지보수 효율을 높였습니다.

---
> **"복잡한 로직을 단순하고 견고하게 설계하는 것을 즐깁니다. 유저에게 즐거운 경험을 주기 위해 끊임없이 고민하는 클라이언트 개발자가 되겠습니다."**
