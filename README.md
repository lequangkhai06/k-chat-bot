# Chạy chat bot

Hướng dẫn này sẽ giúp bạn chạy ứng dụng chat được chứa trong tệp `index.html`.

## Yêu cầu

Đảm bảo bạn có những điều sau:

- Một trình duyệt web (Chrome, Firefox, Safari, v.v.).
- Một máy chủ web cục bộ (như Python's SimpleHTTPServer, Node's http-server, v.v.). Hoặc bạn có thể sử dụng tính năng Live Server từ VSCode.
- Một khóa API từ OpenAI (3.5 / 4) để truy cập API. Hoặc một máy tính xách tay/PC với RAM >8GB.

## Khởi động ứng dụng bằng cách sử dụng OpenAI API

1. **Thiết lập khóa API**

Mở tệp `index.html` và tìm dòng sau:

```html
const chatGPTKey = 'sk-'; // Dán khóa API vào đây
```

Thay `'sk-*****'` bằng khóa API GPT-3 thực tế của bạn.

2. **Khởi động máy chủ cục bộ**

Di chuyển đến thư mục chứa `index.html` và khởi động máy chủ cục bộ của bạn. Ví dụ, nếu bạn đang sử dụng Python's SimpleHTTPServer, bạn có thể khởi động nó bằng lệnh:

```bash
python -m SimpleHTTPServer
```

Nếu bạn đang sử dụng Node's http-server, bạn có thể khởi động nó bằng lệnh:

```bash
http-server
```

3. **Truy cập ứng dụng**

Mở trình duyệt web của bạn và truy cập vào localhost trên cổng mà máy chủ của bạn đang chạy. Ví dụ, nếu máy chủ của bạn đang chạy trên cổng 8000, bạn sẽ truy cập `http://localhost:8000`.

4. **Tương tác với ứng dụng chat**

Bây giờ bạn nên thấy giao diện chat trong trình duyệt của mình. Bạn có thể nhập tin nhắn vào ô đầu vào và nhấn "Gửi" để tương tác với chatbot.

Xin lưu ý rằng đây là một cài đặt đơn giản dành cho việc phát triển và kiểm thử cục bộ. Nó không phù hợp cho một môi trường sản xuất.

## Khởi động ứng dụng bằng cách sử dụng Local API

1. **Tải xuống mô hình**

Tạo một thư mục có tên là `models`, sau đó tải xuống `mistral-7b-openorca.Q4_0.gguf` từ đây <https://huggingface.co/Open-Orca/Mistral-7B-OpenOrca> và đặt vào thư mục `models`.

2. **Cài đặt gói llama_cpp Python**

Theo hướng dẫn tại đây để cài đặt gói llama_cpp Python <https://github.com/abetlen/llama-cpp-python>.

3. **Chạy máy chủ OpenAI cục bộ**

Chạy đoạn mã sau để chạy một máy chủ API OpenAI cục bộ. Máy chủ sẽ chạy ở cổng 8000.

```bash
python3 -m llama_cpp.server --model "./models/mistral-7b-openorca.Q4_0.gguf" --chat_format chatml --n_gpu_layers 1
```

4. **Cập nhật mã ứng dụng chat**

Mở tệp `index.html` và tìm dòng sau

```html
  // Real GPT
  // const OPEN_AI_ENDPOINT = 'https://api.openai.com/v1' // Comment lại dòng này

  // Security, do not deploy this in production
  const chatGPTKey = 'sk-*****'; // API key tại đây

  // Local GPT
  const OPEN_AI_ENDPOINT = 'http://localhost:8000/v1' // Uncomment dòng này
```

Chạy ứng dụng lại. Nó sẽ sử dụng localhost để giao tiếp với API cục bộ.
## Tech Stack

***TailwindCSS, VueJS (Axios)***

