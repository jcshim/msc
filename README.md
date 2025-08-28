# msc
SD msc
## msc1.0 // .exe 삭제
## msc1.1 // .hwp, .doc 제외하고 모두 삭제
## msc2.0 // 
    // 허용 확장자 목록
    const char *allowed[] = {
        ".hwp", ".doc", ".docx",
        ".pdf", ".txt", ".rtf", ".odt",
        ".xls", ".xlsx",
        ".ppt", ".pptx",
        ".pages", ".md"
    };


1. **SD 카드 초기화 & 마운트**

   * `MX_SDMMC1_SD_Init()`으로 SD 카드 컨트롤러를 설정.
   * FATFS (`f_mount`)를 사용해 SD 카드를 파일시스템으로 마운트.

2. **파일 정리 로직**

   * `delete_excluded_files_by_extension()` 함수가 모든 폴더를 재귀적으로 탐색.
   * 확장자가 `.hwp, .doc, .docx, .pdf, .txt` 등 **허용된 목록**에 없으면 `f_unlink()`로 삭제.

3. **USB MSC 초기화**

   * SD 카드 마운트가 성공하면 `MX_USB_DEVICE_Init()`을 호출해 PC에서 USB 저장장치로 보이게 함.

4. **LED 표시**

   * `blink_led()` 함수로 메인 루프에서 PC15 핀에 연결된 LED를 0.5초마다 깜빡임.
   * 에러 시에는 LED를 빠르게 깜빡여 오류를 표시.

👉 **정리**:
부팅 후 SD 카드를 마운트 → 허용된 확장자 외의 파일을 모두 삭제 → USB 저장장치로 연결 → LED로 상태 표시.
흐름도(예: "SD → 검사/삭제 → USB 연결 → LED")
