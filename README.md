# My WebBuild Saving

> Đây là note nhỏ của tớ dùng để lưu lại những thông tin được chia sẻ trên WeBuild
>
> Những nội dung này tớ thấy phù hợp với bản thân và mong muốn lưu lại để tự khám phá
>
> Nếu nó cũng phù hợp với bạn, hãy star/fork để theo dõi hoặc tự ý chỉnh sửa theo ý mình nhé!
>
> Thân,
>
> BeautyOnCode

## 30 days of sharing

> 
> #30daysofsharing là phong trào chia sẻ kiến thức ở WeBuild được khởi xướng bởi "Cậu Làm Vườn"
>

### Frontend
<details>
  <summary>Hiểu về display property</summary>
  
  > By: Cậu Làm Vườn
  >
  > Date: 13/01/2021
  
  #### Context: 

  Khi làm việc với CSS, các bạn sẽ gặp các value quen thuộc cho display là block, inline , inline-block , grid , flex , etc. Nếu tinh ý thì các bạn sẽ nhận ra rằng block và inline element chẳng hạn, sẽ không có special behaviour dành cho children của chúng, trong khi grid item và flex item được xử lí một cách đặc biệt.

  Nguyên nhân là do cái các bạn đang thấy thật ra chỉ là short-hand value. 

  Ở CSS3, display nhận 2 value: outer (define cách chúng tương tác với các element xung quanh) và inner (cách children của chúng tương tác với nhau).

  #### Ví dụ:

  **display: block** là shorthand của display: block flow , nghĩa là bản thân nó behave như một block, children của nó sẽ trở lại flow bình thường của document

  **display: flex** là shorthand của display: block flex , bản thân nó behave như một block (lí do flex container sẽ tự stretch ra full possible width), và children của nó sẽ trở thành flex items.

  Tương tự **display: inline** là shorthand của display: inline flow , **display: inline-block** là shorthand của... display: inline flow-root wait, wat??!! (tại sao có cái value lạ này thì các bạn tự tìm hiểu thêm hoặc chia sẻ ở lần sau nhé :D)

  Lí do chúng ta vẫn còn duy trì single value system là do ở thuở hồng hoang nó đúng là chỉ có 1 value duy nhất. Nên để duy trì backward compatibility promise của the web thì cả 2 system phải cùng tồn tại.

  Hiểu được điều này sẽ giúp các bạn dễ ghi nhớ và không còn cảm thấy hoang mang về behaviour của display nữa.
</details>

  <details>
  <summary>Hãy nói về resolution switching problem</summary>
  
  > By: Cậu Làm Vườn
  >
  > Date: 25/01/2021
  
  Đây là vấn đề còn lại gặp phải khi deal với responsive image (art direction problem đã nói ở lần trước). Do browser sẽ tiến hành fetch image trước khi CSS hay JS kịp được parse (ngay cả trước khi DOM được fully constructed), nên ta phải deal với nó ngay ở markup.
  
  Browser cung cấp cho chúng ta hai để giải quyết:
  
  1. srcset
  
  Như tên gọi, đây là một set các image source, cùng với miêu tả (descriptor) về điều kiện sử dụng của chúng. Qua đó browser sẽ có thể pick image tối ưu nhất cho người dùng. Trong descriptor, chúng ta lại có 2 loại:
  
- Density descriptor. 

Ví dụ: srcset="foo.jpg 1x, foo-large.jpg 2x". Dùng để adapt cho các thiết bị có pixel density cao. Tuy nhiên có thể thấy ngay một hạn chế của descriptor này là không adapt được khi actual width của image thay đổi khi ở các screen size khác nhau.

- Width descriptor. 

Ví dụ: srcset="foo.jpg 480w, foo-large.jpg 1280w. Ở đây chúng ta cho browser biết độ lớn thực tế của bản thân mỗi source mà ta có. Nếu chỉ dừng lại ở đây thì hoàn toàn vô ích. Vì với density descriptor, browser đã biết được trước pixel density của device để có thể pick source tối ưu nhất. Với width descriptor, chúng ta phải cung cấp một dữ kiện nữa là độ lớn cần có của image (khi render), thông qua size attribute.

  2. size
  
Việc specify responsive size ở markup cũng không khác ở CSS mấy. Chúng ta sẽ specify một list các media query và độ lớn của nó khi thỏa mãn media query đó. 

Ví dụ sizes="(min-width: 1280px) 33.3vw, 100vw" (surprisingly, ta còn có thể dùng cả hàm calc trong đó). List này được evaluate từ trái sang phải, giá trị cuối cùng là default.

Kết hợp scrset width descriptor và size, browser đã có đủ đồ chơi để pick đúng ảnh phù hợp nhất.

Và đây là thành quả
```
<img
   srcset="large.jpg 1280w, medium.jpg 640w, small.jpg 320w"
   sizes="(min-width: 1280px) 33.3vw, 100vw"
/>
```

**Note 1:** Còn một vấn đề nữa là type switching problem, nhưng cái đó có thể xử lí dễ dàng bằng picture element y như cách chúng ta xử lí art direction switching vậy. Mọi người tự tìm hiểu thêm)

**Note 2:** Ngoài ra còn 1 try hard mode là làm sao để take into account cả art direction, width, screen width và pixel density. Nếu phải đến bước này thì chúc các bạn may mắn, bình an, mạnh dỏi và minh mẫn :byeanim:

</details>
  
<details>
  <summary>Let's talk about Accessibility (A11y)</summary>
  
  > By: [Huytd - TheFullSnack](https://thefullsnack.com/)
  >
  > Date: 24/01/2021
  
  Một trang web đạt chuẩn accessibility khi nó được thiết kế và phát triển để giúp cho mọi người đều có thể sử dụng được, kể cả những người già, những người khuyết tật hay đơn giản là những người không sử dụng các thiết bị input thông thường trên máy tính.
  
  **Sử dụng được ở đây có nghĩa là:**
  
  - Có thể tiếp nhận được nội dung trên trang web (ví dụ người khiếm thị vẫn có thể nghe được nội dung văn bản, hình ảnh, hoặc người khiếm thính vẫn có thể đọc được các nội dung âm thanh,...)
  
  - Có thể navigate được, và tương tác được với nội dung trên trang web (người không dùng chuột thì vẫn có thể navigate bằng bàn phím, người khiếm thị vẫn có thể navigate hoặc nhập liệu được bằng giọng nói... ví dụ thế)
  
  Tất nhiên accessibility vẫn có thể đem lại rất nhiều lợi ích cho những người không mang khuyết tật, ví dụ keyboard navigation, hoặc người nào thị lực kém, vẫn chỉnh được chữ to lên, high constrast hơn, ai xài kết nối internet kém vẫn có thể sử dụng được trang web mà không gặp trở ngại.
  
  Nếu chỉ có ý định support accessibility một cách cơ bản, bạn có thể focus vào các yếu tố sau:
  - Đừng thay đổi thuộc tính tabIndex của một element nếu không cần thiết
  - Đừng disable cái focus outline của một element (repeat after me: outline: none trong CSS là một tội ác)
  - Nếu phải disable focus outline vì nó quá xấu, thì phải design một cái outline mới đẹp hơn và rõ ràng hơn để bỏ vào
  - Sử dụng semantics HTML tags như <article>, <main>, <nav>,... nếu có thể
  - Với các input element, nên đặt thuộc tính role một cách rõ ràng và chính xác
  - Sử dụng element đúng với mục đích của nó, ví dụ, không dùng thẻ <div> để làm nút bấm (button)
  - Sử dụng các thuộc tính aria-* như aria-label, aria-labelledby, aria-descibedby,... để chú thích và chỉ ra mối quan hệ cho các nội dung/element trên trang web
  
Hiện tại, các hệ điều hành và các trình duyệt đữa đưa ra rất nhiều tiện ích để hỗ trợ accessibility, như là screen readers (đọc nội dung của trang web dựa vào các thuộc tính aria-*, trên MacOS có VoiceOver, trên Windows phải sử dụng các ứng dụng của bên thứ 3 như JAWS), hay các giải pháp điều khiển máy tính thông qua mắt nhìn (built-in của MacOS),... tất cả những giải pháp này đều phụ thuộc rất nhiều vào tiêu chuẩn WCAG.

**Có thể tham khảo thêm các tài liệu sau đây về accessibility:**

- Một vài bước kiểm tra accessibility đơn giản (https://www.w3.org/WAI/test-evaluate/preliminary/)
- Tiêu chuẩn Web Content Accessibility Guidelines (WCAG) https://www.w3.org/WAI/WCAG21/quickref/

  Bên cạnh đối tượng user là những người bình thường, lành lặn, đầy đủ cả tay chân tai mắt mũi mà chúng ta vẫn tưởng tượng ra hằng ngày, ngoài kia vẫn còn rất nhiều người kém may mắn hơn, và họ vẫn có điều kiện để tiêp xúc với công nghệ mỗi ngày, và những user như họ cần được hỗ trợ nhiều hơn từ phía những người trực tiếp làm ra sản phẩm, là frontend developer chúng ta, cho nên, hãy bỏ chút thời gian và công sức để giúp đỡ những user đặc biệt này, mình chắc chắn là bạn sẽ thấy công việc của mình có nhiều ý nghĩa hơn.

  Đặc biệt, đối với những frontend developer đang làm việc tại Mỹ, thì luật pháp quy định mọi trang web đều phải accessible, nên không support hoặc không quan tâm đến a11y có thể coi là phạm pháp.
</details>

<details>
  <summary>Quick note về khái niệm origin trong JavaScript.</summary>
  
  > By: [Huytd - TheFullSnack](https://thefullsnack.com/)
  >
  > Date: 25/01/2021
  
  Một URL thường sẽ có cấu tạo như sau:
  `<scheme>://<host>:<port>/<path>`
  Ví dụ:
  - http://localhost:45848/hello
-   https://thefullsnack.com
  
  Một tập hợp của scheme, host và port sẽ định nghĩa thành một origin. Vậy cho nên khi nói hai nội dung có cùng origin tức là chúng nằm trên cùng scheme + host + port, và tất nhiên nếu một trong 3 yếu tố trên khác nhau thì chúng ta có 2 nội dung không nằm cùng origin với nhau.
  
  Riêng IE, với phong cách nổi loạn thường thấy, sẽ bỏ qua port khi xét origin, nên 2 URL có cùng scheme + host mà khác port thì vẫn tính là same origin.
  
  **Ví dụ về 2 URL có cùng origin:**
  - https://something.com/hello 
  - https://something.com/yolo 
  
  Ví dụ về các URL không có cùng origin với nhau:
  
  // Khác scheme
  - http://abc.com/bobo
  - https://abc.com/koko
  
  // Khác host
  - https://foo.abc.com
  - https://bar.abc.com
  
  // Khác port
  - https://abc.com
  - https://abc.com:8443
  
  Phân biệt được sự khác nhau về origin có thể giúp bạn hiểu và tìm ra giải pháp dễ dàng hơn khi gặp những vấn đề liên quan đến CORS (cross-origin resource sharing), khi truy xuất localStorage, hay khi tìm hiểu về execution context, event loop,...
  
  Đối với các thao tác liên quan đến network connection trên một trang web (HTTP request, hay load image), việc truy xuất cross-origin cho các thao tác sau đây được cho phép:
  
  - Redirect, link, submit form
  - Embedding (như inject content dùng thẻ <script>, <link>, <img>, <video>, <audio>, <object>, <embed>, <iframe>, load font dùng @font-face,...)
  
  Đối với Cookie, thì khác subdomain vẫn được tính là cùng origin.
</details>

<details>
  <summary>Sub title</summary>
  
  > By: Cậu Làm Vườn
  >
  > Date: 25/01/2021
  
  Content go here
</details>

<details>
  <summary>Sub title</summary>
  
  > By: Cậu Làm Vườn
  >
  > Date: 25/01/2021
  
  Content go here
</details>

## Category Name
<details>
  <summary>Sub title</summary>
  Content go here
</details>

