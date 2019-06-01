###
file(GLOB WIN_SRCS win32/*.cxx)
file(GLOB SCITE_SRCS src/*.cxx)


include_directories(
  src
)

add_executable(scite WIN32
  ${WIN_SRCS}
  ${SCITE_SRCS}
  win32/SciTERes.rc
  win32/SciTE.exe.manifest
)

target_link_libraries(scite
  scintilla
  KERNEL32
  USER32
  GDI32
  MSIMG32
  COMDLG32
  COMCTL32
  ADVAPI32
  IMM32
  SHELL32
  OLE32
  OLEAUT32
  UXTHEME
)