// ################################################################# //
// Team9 2021.4 ver.1.0 ############################################ //
// ################################################################# //


공통 =====================================================================

$(window).on('load',function(){
	var cnt;
    if ($.cookie(cookie)) {
		colorPick = $.cookie(cookie)
	}
	bgColorChange(colorList[colorPick]);
    $('.contents').eq(0).show();
    contentScript(0, $('.contents').eq(0));
    
	$('.setContent li').bind('click', function () {
		var idx = $(this).index();
		var page = $('.contents').eq(idx);
        if(cnt != idx){
            cnt = idx;
            contentScript(idx, page);
        }
	});
});

function contentScript(_idx, _page){
    if(typeof(vidoCon) != 'undefined'){vidoCon.stop();};
    switch(_idx){
        case 0:
            
        break;
        case 1:
            
        break;
        case 2:
            
        break;
    }
}

===================================================================================
objectiveContents =================================================================
writeContents =====================================================================
===================================================================================
※ 학습목표 / 직접쓰기

ex)
//학습목표
objectCon = new objectiveContents(_page);
objectCon.init();

//직접쓰기
writeCon = new writeContents(_page);
writeCon.init();


===================================================================================
clickContents =====================================================================
===================================================================================

clickContents(갯수, 해당위치, 버튼모양); 버튼모양 1: 예시, 2: 물음표
clickCon.init(); // 초기화
clickCon.showitem(); // 요소 추가후 나타남

추가기능 1 : 클릭시 새로운 요소가 나타나고 사라짐(토글)
CSS 설정
.clickContent .clickItem {배경 투명하게 설정}
.clickContent .showItem[data-num="0"] {해당 요소가 clickItems과 반대로 나타나고 사라짐 (data-num : 인덱스번호)}

추가기능 2 : 클릭버튼이 1개일 경우 정답보기 버튼 생성
: "anschk_o" 값이 있을 경우 정답버튼 & 정답 사운드
ex) 
clickCon.setAnsBtn("anschk_o");

추가기능 3 : 초성
var choTxt = ["마중물"];

ex) 
clickCon.cho(choTxt)

추가기능 4 : zIndex 설정
clickCon.zIndex(해당 버튼 요소, clickItem 번호);
클릭시 해당 요소의 zIndex를 상위로 올림
※ 타겟 이름 지정은 항상 마지막 순서로

※ 클릭 버튼에 음성 추가하기
clickCon.items.bind('click', function(){
    if($(this).css('opacity') == 0){
        switch($(this).index()){
            case 0:
                contentAdo("1-8-01");
            break;
            case 1:
                contentAdo("1-8-02");
            break;
        }
    }
})

------------------------------------------

ex) 
clickCon = new clickContents(4, _page, 2);
clickCon.init();
clickCon.showitem(); // 추가기능 1
clickCon.setAnsBtn(); // 추가기능 2
clickCon.cho(choTxt); // 추가기능 3
clickCon.zIndex(_page.find('.target'), "1"); // 추가기능 4

===================================================================================
videoPlayer =======================================================================
===================================================================================

<link rel="stylesheet" type="text/css" href="../../common/videopage/css/video.css"/> // css파일 추가

<script src="../../common/videopage/js/video.js"></script> // js파일 추가

<div id="videoFrame" class="videoFrame"></div> // Html 추가


CSS 설정
transform: translateX(-50%); // 가로 가운데 정렬
transform: translateX(-50%) scale(1); // 가로 가운데 정렬 및 축소(확대)

추가기능 1
동영상 탭이동 버튼 삽입

var videoTime = ["01:23", "02:43"];

setVidoTab(버튼 개수, 버튼삽입될 페이지, vidoCon, videoTime(이동시간)); 

CSS 설정
.contents:nth-child(1) .vido_btn[data-num="0"]{버튼 위치, 이미지 설정}
.contents:nth-child(1) .vido_btn[data-num="1"]{버튼 위치, 이미지 설정}
.contents:nth-child(1) .vido_btn[data-num="0"].active{활성화 이미지 설정}
.contents:nth-child(1) .vido_btn[data-num="1"].active{활성화 이미지 설정}

------------------------------------------

ex)
var fileName = 'dummy'; // 영상, 자막 파일명

vidoCon = new videoPlayer($('#videoFrame'));
vidoCon.src = 'inc/media/mp4/'+fileName+'.mp4';
vidoCon.init();
//vidoCon.video.attr('poster','inc/media/mp4/'+fileName+'.png'); // 국어는 동영상 표지 주석처리
setVidoTab(2, _page, vidoCon, videoTime); //추가기능 1



===================================================================================
aniContents =======================================================================
===================================================================================

<div class="ani ani1" data-ado=""></div>
<div class="ani ani2" data-ado=""></div>


aniCon = new aniContents(해당 위치, 말풍선사라지는 여부); true: 모두 보임, false: 모두 사라지고 현재만 나타남
aniCon.init();

CSS 설정
.contents:nth-child(2) .ani1 .ca{기본이미지}
.contents:nth-child(2) .ani1.animotion .ca{클릭 후 이미지}
.contents:nth-child(2) .ani1 .item{말풍선}
.contents:nth-child(2) .ani1 .close{닫기버튼}

------------------------------------------

ex)
aniCon = new aniContents(_page, false); // 국어는 무조건 false
aniCon.init();



===================================================================================
pageingContents ===================================================================
===================================================================================

pageingContents(BN위치);
pageCon.init(); // 초기화
pageCon.setPopUp(버튼위치); // 팝업일경우 BN해당 위치로 이동

pageConEvent_1(pageCon 첫번째 페이지); // 공통으로 실행될 함수
pageCon.wrap.find(".prev, .next, .dot").bind('click',function(){ // 각 이동 버튼 클릭시 공통함수 실행
    pageConEvent_1(pageCon 이동된 페이지); // 공통으로 실행될 함수
})

팝업버튼
<div class="btn" data-num="0"></div> 해당 버튼 클릭시 팝업의 BN 해당 위치로 이동

------------------------------------------
ex) 본문

pageCon = new pageingContents(_page.find('.pageWrap'));
pageCon.init();

pageConEvent_1(pageCon.page.eq(0));
pageCon.wrap.find(".prev, .next, .dot").bind('click',function(){
    pageConEvent_1(pageCon.page.eq(pageCon.currentPage));
});

----------------------
ex) 팝업

<div class="pop pop0"> //팝업 갯수에 따라서 pop0, pop1, pop2...
    <div class="pageWrap">
        <div class="page page1"></div>
        <div class="page page2"></div>
        <div class="page page3"></div>
    </div>
    <div class="close"></div>
</div>

pageCon = new pageingContents($('.pop0 .pageWrap'));
pageCon.init();
pageCon.setPopUp(_page); //팝업

_page.find(".btn").bind('click', function(){
    var p = $(this).attr("data-num");
    pageConEvent_1(pageCon.page.eq(p));
});
pageCon.wrap.find(".prev, .next, .dot").bind('click',function(){
    pageConEvent_1(pageCon.page.eq(pageCon.currentPage));
});

----------------------
ex) 해당 페이지별 작업 내용

function pageConEvent_1(_page){ // 공통으로 실행될 함수
    switch(_page.index()){ //page마다 기능이 다를 경우 사용
        case 0:
        break;
        case 1:
        break;
    }
}

===================================================================================
oxContents ========================================================================
===================================================================================
※ 보기가 O, X 2개일 경우에만 사용

var ox = [정답];

oxCon = new oxContents(해당 위치, 해당 정답);
oxCon.init(); // 초기화

CSS 설정
.o_item{O 이미지}
.x_item{X 이미지}
.o_item.dis{O 오답 이미지}
.x_item.dis{X 오답 이미지}
.o_item.cor{O 정답 이미지}
.x_item.cor{X 정답 이미지}

------------------------------------------

ex)
var ox = ["O", "X", "O", "O", "X"];

oxCon = new oxContents(_page, ox[_page.index()]);
oxCon.init();


===================================================================================
quizContents ======================================================================
===================================================================================
※ 보기가 여러개일 경우 사용,
※ 4, 5지선다, 이미지 클릭, 박스 클릭 등등
※ 다중정답 가능

var quizItem = {
    exp: ['보기1', '보기2', '보기3', '보기4'], // 보기 텍스트, 이미지 사용시 공백, 갯수 만큼 배열
    ans: ['1', '3'], // 정답, 다중 정답
};

quizCon = new quizContents(해당 페이지, 보기-정답 배열);
quizCon.init();

CSS 설정
// 텍스트 사용시
.contents:nth-child(2) .bogi li{ 
    padding-left: 75px;
    margin-bottom: 55px;
}
.quizGroup li .icon{정답 동그라미}


// 이미지 사용시
.contents:nth-child(1) .bogi li:nth-child(1){기본이미지}
.contents:nth-child(1) .bogi li.on:nth-child(1){정답이미지}
.contents:nth-child(1) .bogi li.off:nth-child(1){오답이미지}
.contents:nth-child(1) .bogi li.on:nth-child(1) .icon{정답 동그라미}
.contents:nth-child(1) .bogi li.off:nth-child(1) .icon{오답 동그라미}


추가기능 1
오답풀이
CSS 설정 : 여백 없는 이미지로 만들어야 함.
.contents:nth-child(1) .quizExp .exp_txt{
    width: 1277px;
    height: 200px;
    background: url(../images/10/exp_1.png) no-repeat;
}

------------------------------------------

ex)
var quizItem = {
    exp: ['다른 사람을 배려하는 자세', '자신을 이해하고 존중하는 자세', '새로운 일에 용기 있게 도전하는 자세'],
    ans: ['2'],
};

quizCon = new quizContents(_page, quizItem);
quizCon.init();
quizCon.explain(); // 추가기능 1



===================================================================================
popupContents =====================================================================
===================================================================================
※ BN가 없는 팝업 기능

popCon = new popupContents(해당 페이지, 버튼(팝업) 개수);
popCon.init();

CSS 설정
.contents:nth-child(1) .popup_btn{버튼 위치 및 크기}
.contents:nth-child(1) .popup{background: rgba(0,0,0,0.7) url(팝업 이미지)}

------------------------------------------

ex)
popCon = new popupContents(_page, 1);
popCon.init();


===================================================================================
lineQuizContent ===================================================================
===================================================================================
※ 선긋기

<script src="../../common/js/linequiz.js"></script>

lineCon = new lineQuizContents(해당위치, 왼쪽 개수, 오른쪽 개수, 정답, {옵션});
lineCon.init();

옵션
_page: _page 필수 삽입
overlap: 한 점에 라인을 중복 가능 여부 (true : 중복 가능, false : 중복 불가능)


CSS 설정
.contents:nth-child(1) .quizSec .quizArea .leftLine .ansArea {왼쪽 포인터 위치}
.contents:nth-child(1) .quizSec .quizArea .leftLine .ansArea:nth-child(2) {왼쪽 포인터 위치}
.contents:nth-child(1) .quizSec .quizArea .leftLine .ansArea:nth-child(3) {왼쪽 포인터 위치}

.contents:nth-child(1) .quizSec .quizArea .rightLine .r_item {오른쪽 포인터 위치}
.contents:nth-child(1) .quizSec .quizArea .rightLine .r_item:nth-child(2) {오른쪽 포인터 위치}
.contents:nth-child(1) .quizSec .quizArea .rightLine .r_item:nth-child(3) {오른쪽 포인터 위치}

------------------------------------------

ex)
var quizItem = ["0_1", "1_2", "2_0"];

lineCon = new lineQuizContents(_page, 3, 3, quizItem, {
    _page: _page,
    overlap: true;
});
lineCon.init();
※ _page: _page 필수 삽입




===================================================================================
helpContents ======================================================================
===================================================================================
※ 도움말 이미지 사용

helpCon = new helpContents(해당 위치);
helpCon.init();

CSS 설정
여백 없는 이미지로 만들어야 함.
.contents:nth-child(2) .con{
    height: 228px;
    background: url(../images/06/help_1.png) center bottom no-repeat;
}
------------------------------------------

ex)
helpCon = new helpContents(_page);
helpCon.init();



===================================================================================
dragContents ======================================================================
===================================================================================
※ 드래그 / 드롭을 이미지 사용할 경우 dragItems 정답을 숫자로 사용하고 CSS설정해줌
   (text-indent: -9999px -> 추가)

<script src="../../common/js/jquery.ui.drag.js"></script>
<script src="../../common/js/jquery.ui.touch-punch.min.js"></script>

dragCon = new dragContents(해당 위치, 드래그앤드롭 정답, {옵션}); 

옵션
random: "1", //랜덤정답 "1": 정오답, "2": 정답 없는 랜덤정답, "3": 정답 있는 랜덤정답
answer: function(_val){
    if(_val){
        //정답일 경우
    }else{
        //오답일 경우
    }
} //정답, 오답 콜백함수
clickAnsbtn: function(_val){
    if(_val){
        //정답보기를 클릭한 경우
    }else{
        //다시하기를 클릭한 경우
    }
}; //정답버튼 클릭 콜백함수

CSS 설정
.contents:nth-child(1) .dragArea{드래그위치}
.contents:nth-child(1) .dropArea{드롭위치}
.contents:nth-child(1) .dragArea .dragItem{드래그 버튼 설정}
.contents:nth-child(1) .dropArea .dropCode{드롭 버튼 설정}
.contents:nth-child(1) .dropArea .dropCode.ans span{정답일경우 가로세로 가운데 정렬하기 위해 만듬(텍스트를 span으로 감쌈)}
------------------------------------------

ex)
var dragItems = {
    drop: ['정직'],
    drag: ['정직', '모범', '사랑', '양심'],
}

dragCon = new dragContents(_page, dragItems, {옵션});
dragCon.init();



===================================================================================
scrollContents ======================================================================
===================================================================================

<link rel="stylesheet" type="text/css" href="../../common/css/jquery.mCustomScrollbar.css" />

<script src="../../common/js/jquery.mCustomScrollbar.js"></script>

scrollCon = new scrollContents(생성위치, 스크롤 위치); 
scrollCon.init();

CSS 설정
.contents:nth-child(2) .scrollGroup {스크롤 위치}
.contents:nth-child(2) .scrollGroup .item{ 
    position: relative;
    width: 전체이미지 폭;
    height: 전체이미지 높이;
    background: url(../images/05/pop_01.png) no-repeat;
}

------------------------------------------

ex)
scrollCon = new scrollContents(_page, "left"); 
scrollCon.init();


===================================================================================
mapContents ======================================================================
===================================================================================

mapCon = new mapContents(해당 위치, 가로픽셀, 세로픽셀, 지도안에 버튼이 있는경우);
mapCon.init();

CSS 설정
.contents:nth-child(1) .mapZoom{확대축소 위치}
.contents:nth-child(1) .mapZoom .map{확대축소될 이미지}
.contents:nth-child(1) .mapZoom .innerbtn{안쪽에 버튼}

------------------------------------------

ex)
mapCon = new mapContents(_page, 1053, 789, false);
mapCon.init();



===================================================================================
 ======================================================================
===================================================================================


------------------------------------------









===================================================================================
 ======================================================================
===================================================================================


------------------------------------------














