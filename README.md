# overlay
ovcerla yfor my yt vid  how to make a fortnite cheat pt1







//overlay
IDirect3D9Ex* p_object = NULL;
IDirect3DDevice9Ex* p_device = NULL;
D3DPRESENT_PARAMETERS p_params = { NULL };
MSG messager = { NULL };
HWND my_wnd = NULL;
HWND game_wnd = NULL;




HRESULT directx_init()
{
	if (FAILED(Direct3DCreate9Ex(D3D_SDK_VERSION, &p_object))) exit(3);

	ZeroMemory(&p_params, sizeof(p_params));
	p_params.Windowed = TRUE;
	p_params.SwapEffect = D3DSWAPEFFECT_DISCARD;
	p_params.hDeviceWindow = my_wnd;
	p_params.MultiSampleQuality = D3DMULTISAMPLE_NONE;
	p_params.BackBufferFormat = D3DFMT_A8R8G8B8;
	p_params.BackBufferWidth = settings::width;
	p_params.BackBufferHeight = settings::height;
	p_params.EnableAutoDepthStencil = TRUE;
	p_params.AutoDepthStencilFormat = D3DFMT_D16;
	p_params.PresentationInterval = D3DPRESENT_INTERVAL_DEFAULT;

	if (FAILED(p_object->CreateDeviceEx(D3DADAPTER_DEFAULT, D3DDEVTYPE_HAL, my_wnd, D3DCREATE_HARDWARE_VERTEXPROCESSING, &p_params, 0, &p_device)))
	{
		p_object->Release();
		exit(4);
	}

	ImGui::CreateContext();
	ImGui_ImplWin32_Init(my_wnd);
	ImGui_ImplDX9_Init(p_device);

	ImGuiIO& io = ImGui::GetIO(); (void)io;
	ImFontAtlas* fontAtlas = io.Fonts;
	ImFontConfig arialConfig;
	arialConfig.FontDataOwnedByAtlas = false;
	ImFont* arialFont = fontAtlas->AddFontFromFileTTF("c:\\Windows\\Fonts\\arialbd.ttf", 15.0f, &arialConfig);
	io.Fonts = fontAtlas;
	io.IniFilename = 0;

	ImGuiStyle* style = &ImGui::GetStyle();

	// Set global style properties
	style->WindowPadding = ImVec2(8, 8);
	style->FramePadding = ImVec2(5, 5);
	style->ItemSpacing = ImVec2(6, 4);
	style->ItemInnerSpacing = ImVec2(6, 4);
	style->IndentSpacing = 25.0f;
	style->ScrollbarSize = 15.0f;
	style->GrabMinSize = 10.0f;
	style->WindowBorderSize = 0.0f;
	style->ChildBorderSize = 0.0f;
	style->PopupBorderSize = 0.0f;
	style->FrameBorderSize = 0.0f;
	style->TabBorderSize = 0.0f;
	style->WindowRounding = 6.0f;
	style->ChildRounding = 6.0f;
	style->FrameRounding = 6.0f;
	style->PopupRounding = 6.0f;
	style->ScrollbarRounding = 9.0f;
	style->GrabRounding = 6.0f;
	style->LogSliderDeadzone = 4.0f;
	style->TabRounding = 6.0f;

	// Set colors to match the image
	style->Colors[ImGuiCol_Text] = ImVec4(1.00f, 1.00f, 1.00f, 1.00f); // White text
	style->Colors[ImGuiCol_TextDisabled] = ImVec4(0.50f, 0.50f, 0.50f, 1.00f);
	style->Colors[ImGuiCol_WindowBg] = ImVec4(0.12f, 0.09f, 0.16f, 0.94f); // Dark purple background
	style->Colors[ImGuiCol_ChildBg] = ImVec4(0.12f, 0.09f, 0.16f, 0.94f); // Dark purple background
	style->Colors[ImGuiCol_PopupBg] = ImVec4(0.08f, 0.08f, 0.08f, 0.94f);
	style->Colors[ImGuiCol_Border] = ImVec4(0.43f, 0.43f, 0.50f, 0.50f);
	style->Colors[ImGuiCol_BorderShadow] = ImVec4(0.00f, 0.00f, 0.00f, 0.00f);
	style->Colors[ImGuiCol_FrameBg] = ImVec4(0.16f, 0.13f, 0.22f, 1.00f); // Slightly lighter purple for frames
	style->Colors[ImGuiCol_FrameBgHovered] = ImVec4(0.20f, 0.17f, 0.27f, 1.00f);
	style->Colors[ImGuiCol_FrameBgActive] = ImVec4(0.24f, 0.20f, 0.32f, 1.00f);
	style->Colors[ImGuiCol_TitleBg] = ImVec4(0.12f, 0.09f, 0.16f, 1.00f); // Dark purple title bar
	style->Colors[ImGuiCol_TitleBgActive] = ImVec4(0.12f, 0.09f, 0.16f, 1.00f);
	style->Colors[ImGuiCol_TitleBgCollapsed] = ImVec4(0.00f, 0.00f, 0.00f, 0.51f);
	style->Colors[ImGuiCol_MenuBarBg] = ImVec4(0.14f, 0.14f, 0.14f, 1.00f);
	style->Colors[ImGuiCol_ScrollbarBg] = ImVec4(0.02f, 0.02f, 0.02f, 0.53f);
	style->Colors[ImGuiCol_ScrollbarGrab] = ImVec4(0.31f, 0.31f, 0.31f, 1.00f);
	style->Colors[ImGuiCol_ScrollbarGrabHovered] = ImVec4(0.41f, 0.41f, 0.41f, 1.00f);
	style->Colors[ImGuiCol_ScrollbarGrabActive] = ImVec4(0.51f, 0.51f, 0.51f, 1.00f);
	style->Colors[ImGuiCol_CheckMark] = ImVec4(0.58f, 0.39f, 0.82f, 1.00f); // Purple checkmark
	style->Colors[ImGuiCol_SliderGrab] = ImVec4(0.58f, 0.39f, 0.82f, 1.00f); // Purple slider grab
	style->Colors[ImGuiCol_SliderGrabActive] = ImVec4(0.70f, 0.50f, 0.90f, 1.00f);
	style->Colors[ImGuiCol_Button] = ImVec4(0.58f, 0.39f, 0.82f, 1.00f); // Purple button
	style->Colors[ImGuiCol_ButtonHovered] = ImVec4(0.70f, 0.50f, 0.90f, 1.00f);
	style->Colors[ImGuiCol_ButtonActive] = ImVec4(0.47f, 0.31f, 0.66f, 1.00f);
	style->Colors[ImGuiCol_Header] = ImVec4(0.58f, 0.39f, 0.82f, 1.00f); // Purple header
	style->Colors[ImGuiCol_HeaderHovered] = ImVec4(0.70f, 0.50f, 0.90f, 1.00f);
	style->Colors[ImGuiCol_HeaderActive] = ImVec4(0.47f, 0.31f, 0.66f, 1.00f);
	style->Colors[ImGuiCol_Separator] = ImVec4(0.43f, 0.43f, 0.50f, 0.50f);
	style->Colors[ImGuiCol_SeparatorHovered] = ImVec4(0.10f, 0.40f, 0.75f, 0.78f);
	style->Colors[ImGuiCol_SeparatorActive] = ImVec4(0.10f, 0.40f, 0.75f, 1.00f);
	style->Colors[ImGuiCol_ResizeGrip] = ImVec4(0.26f, 0.59f, 0.98f, 0.25f);
	style->Colors[ImGuiCol_ResizeGripHovered] = ImVec4(0.26f, 0.59f, 0.98f, 0.67f);
	style->Colors[ImGuiCol_ResizeGripActive] = ImVec4(0.26f, 0.59f, 0.98f, 0.95f);
	style->Colors[ImGuiCol_Tab] = ImVec4(0.16f, 0.13f, 0.22f, 0.86f); // Darker purple for inactive tabs
	style->Colors[ImGuiCol_TabHovered] = ImVec4(0.58f, 0.39f, 0.82f, 0.80f); // Purple for hovered tabs
	style->Colors[ImGuiCol_TabActive] = ImVec4(0.58f, 0.39f, 0.82f, 1.00f); // Purple for active tabs
	style->Colors[ImGuiCol_TabUnfocused] = ImVec4(0.07f, 0.10f, 0.15f, 0.97f);
	style->Colors[ImGuiCol_TabUnfocusedActive] = ImVec4(0.14f, 0.26f, 0.42f, 1.00f);
	style->Colors[ImGuiCol_PlotLines] = ImVec4(0.61f, 0.61f, 0.61f, 1.00f);
	style->Colors[ImGuiCol_PlotLinesHovered] = ImVec4(1.00f, 0.43f, 0.35f, 1.00f);
	style->Colors[ImGuiCol_PlotHistogram] = ImVec4(0.90f, 0.70f, 0.00f, 1.00f);
	style->Colors[ImGuiCol_PlotHistogramHovered] = ImVec4(1.00f, 0.60f, 0.00f, 1.00f);
	style->Colors[ImGuiCol_TableHeaderBg] = ImVec4(0.19f, 0.19f, 0.20f, 1.00f);
	style->Colors[ImGuiCol_TableBorderStrong] = ImVec4(0.31f, 0.31f, 0.35f, 1.00f);
	style->Colors[ImGuiCol_TableBorderLight] = ImVec4(0.23f, 0.23f, 0.25f, 1.00f);
	style->Colors[ImGuiCol_TableRowBg] = ImVec4(0.00f, 0.00f, 0.00f, 0.00f);
	style->Colors[ImGuiCol_TableRowBgAlt] = ImVec4(1.00f, 1.00f, 1.00f, 0.06f);
	style->Colors[ImGuiCol_TextSelectedBg] = ImVec4(0.26f, 0.59f, 0.98f, 0.35f);
	style->Colors[ImGuiCol_DragDropTarget] = ImVec4(1.00f, 1.00f, 0.00f, 0.90f);
	style->Colors[ImGuiCol_NavHighlight] = ImVec4(0.26f, 0.59f, 0.98f, 1.00f);
	style->Colors[ImGuiCol_NavWindowingHighlight] = ImVec4(1.00f, 1.00f, 1.00f, 0.70f);
	style->Colors[ImGuiCol_NavWindowingDimBg] = ImVec4(0.80f, 0.80f, 0.80f, 0.20f);
	style->Colors[ImGuiCol_ModalWindowDimBg] = ImVec4(0.80f, 0.80f, 0.80f, 0.35f);



	p_object->Release();
	return S_OK;
}





void create_overlay()
{
	WNDCLASSEXA wcex = {
		sizeof(WNDCLASSEXA),
		0,
		DefWindowProcA,
		0,
		0,
		0,
		LoadIcon(0, IDI_APPLICATION),
		LoadCursor(0, IDC_ARROW),
		0,
		0,
		skCrypt("Overlay"),
		LoadIcon(0, IDI_APPLICATION)
	};

	ATOM rce = RegisterClassExA(&wcex);
	RECT rect;
	GetWindowRect(GetDesktopWindow(), &rect);

	my_wnd = gui::create_window_in_band(0, rce, skCrypt(L"Overlay"),
		WS_POPUP | WS_EX_TOPMOST,
		rect.left, rect.top,
		rect.right - rect.left, rect.bottom - rect.top,
		0, 0, wcex.hInstance, 0, gui::ZBID_UIACCESS);

	SetWindowLong(my_wnd, GWL_EXSTYLE, WS_EX_LAYERED | WS_EX_TRANSPARENT | WS_EX_TOOLWINDOW);
	SetLayeredWindowAttributes(my_wnd, RGB(0, 0, 0), 255, LWA_ALPHA);

	MARGINS margin = { -1 };
	DwmExtendFrameIntoClientArea(my_wnd, &margin);

	ShowWindow(my_wnd, SW_SHOWDEFAULT);
	UpdateWindow(my_wnd);
}













HWND get_process_wnd(uint32_t pid)
{

	std::pair<HWND, uint32_t> params = { 0, pid };
	BOOL bresult = EnumWindows([](HWND hwnd, LPARAM lparam) -> BOOL
		{
			auto pparams = (std::pair<HWND, uint32_t>*)(lparam);
			uint32_t processid = 0;
			if (GetWindowThreadProcessId(hwnd, reinterpret_cast<LPDWORD>(&processid)) && processid == pparams->second)
			{
				SetLastError((uint32_t)-1);
				pparams->first = hwnd;
				return FALSE;
			}
			return TRUE;
		}, (LPARAM)&params);

	if (!bresult && GetLastError() == -1 && params.first) return params.first;

	return 0;
}




WPARAM render_loop()
{

	static RECT old_rc;
	auto lastFrameTime = std::chrono::high_resolution_clock::now();

	bool running = true;
	while (running)
	{
		while (PeekMessage(&messager, my_wnd, 0, 0, PM_REMOVE))
		{
			TranslateMessage(&messager);
			DispatchMessage(&messager);
			if (messager.message == WM_QUIT)
			{
				running = false;
			}
		}

		if (!running) break;

		if (game_wnd == NULL) exit(0);

		HWND active_wnd = GetForegroundWindow();
		if (active_wnd == game_wnd)
		{
			HWND target_wnd = GetWindow(active_wnd, GW_HWNDPREV);
			SetWindowPos(my_wnd, target_wnd, 0, 0, 0, 0, SWP_NOMOVE | SWP_NOSIZE);
		}
		else
		{
			game_wnd = get_process_wnd(requests::process_id);
			Sleep(250);
		}

		RECT rc;
		POINT xy;
		ZeroMemory(&rc, sizeof(RECT));
		ZeroMemory(&xy, sizeof(POINT));
		rc.left = xy.x;
		rc.top = xy.y;
		ImGuiIO& io = ImGui::GetIO();
		io.DeltaTime = 1.0f / 60.0f;
		POINT p;
		GetCursorPos(&p);
		io.MousePos.x = p.x - xy.x;
		io.MousePos.y = p.y - xy.y;

		if (GetAsyncKeyState(0x1))
		{
			io.MouseDown[0] = true;
			io.MouseClicked[0] = true;
			io.MouseClickedPos[0].x = io.MousePos.x;
			io.MouseClickedPos[0].x = io.MousePos.y;
		}
		else
		{
			io.MouseDown[0] = false;
		}

		if (rc.left != old_rc.left || rc.right != old_rc.right || rc.top != old_rc.top || rc.bottom != old_rc.bottom)
		{
			old_rc = rc;
			settings::width = rc.right;
			settings::height = rc.bottom;
			p_params.BackBufferWidth = settings::width;
			p_params.BackBufferHeight = settings::height;
			SetWindowPos(my_wnd, (HWND)0, xy.x, xy.y, settings::width, settings::height, SWP_NOREDRAW);
			p_device->Reset(&p_params);
		}


		ImGui_ImplDX9_NewFrame();
		ImGui_ImplWin32_NewFrame();
		ImGui::NewFrame();
		{
			features();
			render_menu();
		}
		ImGui::EndFrame();
		ImGui::Render();

		p_device->SetRenderState(D3DRS_ZENABLE, false);
		p_device->SetRenderState(D3DRS_ALPHABLENDENABLE, false);
		p_device->SetRenderState(D3DRS_SCISSORTESTENABLE, false);
		p_device->Clear(0, 0, D3DCLEAR_TARGET, D3DCOLOR_ARGB(0, 0, 0, 0), 1.0f, 0);

		if (p_device->BeginScene() >= 0)
		{
			ImGui_ImplDX9_RenderDrawData(ImGui::GetDrawData());
			p_device->EndScene();
		}

		HRESULT result = p_device->Present(0, 0, 0, 0);
		if (result == D3DERR_DEVICELOST && p_device->TestCooperativeLevel() == D3DERR_DEVICENOTRESET)
		{
			ImGui_ImplDX9_InvalidateDeviceObjects();
			p_device->Reset(&p_params);
			ImGui_ImplDX9_CreateDeviceObjects();
		}


		auto currentFrameTime = std::chrono::high_resolution_clock::now();
		std::chrono::duration<float, std::milli> frameDuration = currentFrameTime - lastFrameTime;
		lastFrameTime = currentFrameTime;



	}

	ImGui_ImplDX9_Shutdown();
	ImGui_ImplWin32_Shutdown();
	ImGui::DestroyContext();

	if (p_device != 0)
	{
		p_device->EndScene();
		p_device->Release();
	}

	if (p_object != 0) p_object->Release();

	DestroyWindow(my_wnd);

	return messager.wParam;
}






