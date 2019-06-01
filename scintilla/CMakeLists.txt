
file(GLOB LEXERS_SRCS lexers/*.cxx)
file(GLOB LEXLIB_SRCS lexlib/*.cxx)
file(GLOB SCINTILLA_SRCS src/*.cxx)

add_library(scintilla STATIC
  ${LEXERS_SRCS}
  ${LEXLIB_SRCS}
  ${SCINTILLA_SRCS}
  win32/HanjaDic.cxx
  win32/PlatWin.cxx
  win32/ScintillaWin.cxx
)