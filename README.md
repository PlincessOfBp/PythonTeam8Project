def draw(self):
    self.screen.fill(BLACK)
    self.all_sprites.draw(self.screen)
    self.draw_ui()
    pg.display.flip()


def draw_ui(self):
    if self.screen_mode == 0:
        # 로고 화면
        self.screen.fill(WHITE)
        try:
            self.screen.blit(self.spr_printed, (
                (WIDTH - self.spr_printed.get_width()) // 2, (HEIGHT - self.spr_printed.get_height()) // 2))
        except AttributeError:
            self.draw_text("RhythmGame", 40, WIDTH // 2, HEIGHT // 2, center=True)

    elif self.screen_mode == 1:
        # 메인 메뉴
        self.draw_text("메인 메뉴", 40, WIDTH // 2, HEIGHT // 2 - 40, center=True)
        self.draw_text("ENTER - 곡 선택", 24, WIDTH // 2, HEIGHT // 2, center=True)

    elif self.screen_mode == 2:
        # 곡 선택 화면
        self.draw_text("곡 선택", 40, WIDTH // 2, HEIGHT // 2 - 80, center=True)

        # 현재 선택된 곡 강조
        y_start = HEIGHT // 2 - 40
        for i, song in enumerate(self.song_list, start=1):
            color = RED if i == self.song_select else WHITE
            self.draw_text(song, 28, WIDTH // 2, y_start + (i - self.song_select) * 30, color=color, center=True)

        self.draw_text("↑↓로 곡 선택", 20, WIDTH // 2, HEIGHT - 60, center=True)
        self.draw_text("ENTER - 플레이 시작", 20, WIDTH // 2, HEIGHT - 30, center=True)

    elif self.screen_mode == 3:
        # 플레이 화면
        self.draw_text(f"점수: {self.score}", 28, 10, 10)
        # 게임 진행 시간 표시
        time_m = self.elapsed_time // 60000
        time_s = (self.elapsed_time // 1000) % 60
        time_str = f"{time_m}:{time_s:02d}"
        self.draw_text(time_str, 28, WIDTH - 120, 10)

    elif self.screen_mode == 4:
        # 결과 화면
        self.draw_text("결과 화면", 40, WIDTH // 2, HEIGHT // 2 - 80, center=True)
        self.draw_text(f"최종 점수: {self.score}", 36, WIDTH // 2, HEIGHT // 2 - 30, center=True)
        self.draw_text("ENTER - 메인으로", 24, WIDTH // 2, HEIGHT // 2 + 30, center=True)


def draw_text(self, text, size, x, y, color=WHITE, center=False):
    font = pg.font.SysFont("malgun", size)
    text_surface = font.render(text, True, color)
    text_rect = text_surface.get_rect()
    if center:
        text_rect.center = (x, y)
    else:
        text_rect.topleft = (x, y)
    self.screen.blit(text_surface, text_rect)
