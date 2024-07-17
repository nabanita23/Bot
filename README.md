import {createSlice, isAnyOf, PayloadAction} from "@reduxjs/toolkit";
import {Access, AccessMode} from "~components/interfaces/WorkflowInterface";
import {
  editActiveWorkflowThunk,
  editDraftWorkflowThunk,
  enableFormCapabilityUsageThunk,
  evaluateAccessThunk,
  previewActiveWorkflowThunk
} from "~components/statemanagement/AsyncThunk";

const initialState :Access = {
  mode:AccessMode.READ_ONLY,
  wizardUpdateState:0
}
const accessSlice = createSlice({
   name:'accessStore',
   initialState,
  reducers:{
    setAccessMode: (state,action:PayloadAction<AccessMode>) => {
      state.mode = action.payload
      state.wizardUpdateState = (state.wizardUpdateState ?? 0)+1
    },
    updateWizardState:(state) => {
      state.wizardUpdateState = (state.wizardUpdateState ?? 0)+1
    },
    resetAccess:(state)=>{
       state.wizardUpdateState = 0
    }
  },
  extraReducers:(builder => {
     builder
       .addCase(enableFormCapabilityUsageThunk.fulfilled,(state) => {
       state.mode = AccessMode.EDIT
       state.wizardUpdateState = (state.wizardUpdateState ?? 0)+1
     })
       .addCase(editDraftWorkflowThunk.fulfilled,(state,action)=>{
         state.mode = action.payload.accessMode ?? AccessMode.READ_ONLY
         state.wizardUpdateState = (state.wizardUpdateState ?? 0)+1
       })
       .addCase(evaluateAccessThunk.fulfilled,(state, action)=> {
           state.wizardUpdateState = 0
           state.mode = action.payload ? AccessMode.EDIT : AccessMode.READ_ONLY
       })
       .addCase(evaluateAccessThunk.rejected,(state)=> {
         state.wizardUpdateState = 0
         state.mode = AccessMode.READ_ONLY
       })
       .addMatcher(isAnyOf(editActiveWorkflowThunk.fulfilled,previewActiveWorkflowThunk.fulfilled),(state,action)=> {
         state.mode = action?.payload?.accessMode ?? AccessMode.READ_ONLY
         state.wizardUpdateState = (state.wizardUpdateState ?? 0)+1
       })
  })
})

export const {setAccessMode,resetAccess,updateWizardState} = accessSlice.actions
export default accessSlice.reducer
