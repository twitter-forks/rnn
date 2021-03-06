SET(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

CMAKE_MINIMUM_REQUIRED(VERSION 2.6 FATAL_ERROR)
CMAKE_POLICY(VERSION 2.6)

FIND_PACKAGE(Torch REQUIRED)

SET(BUILD_STATIC YES) # makes sure static targets are enabled in ADD_TORCH_PACKAGE

SET(CMAKE_C_FLAGS "--std=c99 -pedantic -Werror -Wall -Wextra -Wno-unused-function -D_GNU_SOURCE ${CMAKE_C_FLAGS}")
SET(src
   init.c
)
SET(luasrc
  init.lua
  AbstractRecurrent.lua
  AbstractSequencer.lua
  BiSequencer.lua
  BiSequencerLM.lua
  CopyGrad.lua
  Dropout.lua
  ExpandAs.lua
  FastLSTM.lua
  GRU.lua
  LinearNoBias.lua
  LookupTableMaskZero.lua
  LSTM.lua
  MaskZero.lua
  MaskZeroCriterion.lua
  Module.lua
  Mufuru.lua
  NormStabilizer.lua
  Padding.lua
  Recurrence.lua
  Recurrent.lua
  RecurrentAttention.lua
  recursiveUtils.lua
  Recursor.lua
  Repeater.lua
  RepeaterCriterion.lua
  SAdd.lua
  SeqBRNN.lua
  SeqGRU.lua
  SeqLSTM.lua
  SeqLSTMP.lua
  SeqReverseSequence.lua
  Sequencer.lua
  SequencerCriterion.lua
  TrimZero.lua
  ZeroGrad.lua
  test/bigtest.lua
  test/test.lua
  VariableLength.lua
)

ADD_TORCH_PACKAGE(rnn "${src}" "${luasrc}" "An RNN library for Torch")

TARGET_LINK_LIBRARIES(rnn luaT TH)

SET_TARGET_PROPERTIES(rnn_static PROPERTIES COMPILE_FLAGS "-fPIC -DSTATIC_TH")

INSTALL(FILES ${luasrc} DESTINATION "${Torch_INSTALL_LUA_PATH_SUBDIR}/rnn")