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
> Some description
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
  
## Category Name
<details>
  <summary>Sub title</summary>
  
  > By: Cậu Làm Vườn
  >
  > Date: 25/01/2021
  
  Content go here
</details>
