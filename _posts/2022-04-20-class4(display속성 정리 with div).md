---

---

# 2022. 04.19. 수업내용 정리 #1/2

## display 속성 정리 with div tag



+ display 속성 정리

  * 블록(block)

    속성값이 블록인 요소는 언제나 새로운 라인에서 시작하며, 해당 라인의 모든 너비(width)를 차지합니다.  <br>

    <img src="../images/2022-04-20-fourth/display-block.png" alt="display-block" style="zoom:70%;" />

    <br>

  * 인라인(inline)

    새로운 라인(line)에서 시작하는 것이 아니고 요소의 너비도 해당 라인 전체가 아닌 해당 HTML 요소(아래의 이미지 상에서는 div 내부를 의미)의 내용<br>(content)만큼 차지합니다. <br>

    아래의 id="box2"의 경우 div안에 내용(content)이 없기 때문에 우측 웹페이지 상에서는 나타나지 않습니다.<br>

    <img src="../images/2022-04-20-fourth/display-inline.png" alt="display-inline" style="zoom:70%;" />

    <br>

  * 인라인 블록(inline-block)

    해당 요소 자체는 인라인(inline)처럼 동작합니다. <br>

    하지만 요소 내부에서는 블록(block)처럼 행동합니다. <br>

    <img src="../images/2022-04-20-fourth/display-inline-block.png" alt="display-inline-block" style="zoom:70%;" />

    

  * 논(none)

    HTML 요소를 숨기기 위해서는 display 속성값을 none으로 설정하면 됩니다.<br>

    설정 후, 해당 요소는 웹 페이지에 더 이상 나타나지 않으며, 웹 페이지의 레이아웃에도 영향을 미치지 않습니다.<br>

    또한 visibility 속성값을 hidden으로 설정해도 HTML요소를 숨길 수 있습니다.<br>

    * display : none VS visibility : hidden

      display : none 은 해당 요소는 웹페이지에 더 이상 나타나지 않으며, 레이아웃에도 영향을 미치지 않습니다.<br>

      visibility : hidden 은 요소가 웹페이지에 나타나지 않지만, 레이아웃 내에는 여전히 존재하게 되며 아래의 이미지는 두 속성의 비교를 나타낸 것입니다. <br>

      <img src="../images/2022-04-20-fourth/display-none,visibility.png" alt="display-none,visibility" style="zoom:70%;" />

      <br>

      <br>

      이번에는 display의 기본 속성만 정리해보았고 다음 편에는 float 속성에 대해 정리하겠습니다. <br>

      display에는 flex, grid 와 같이 현업에서 자주 쓰이는 속성이 있지만, 좀 더 정리가 필요하다고 판단해 따로 정리하여 게시할 예정입니다. 

    

    

    
