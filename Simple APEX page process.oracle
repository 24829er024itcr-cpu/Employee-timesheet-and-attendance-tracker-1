-- APEX Page Process: Insert Attendance
-- Trigger: After Submit
-- Assumes APEX page items: :P1_EMPLOYEE_ID, :P1_DATE, :P1_CLOCK_IN, :P1_CLOCK_OUT, :P1_STATUS, :P1_REMARKS

BEGIN
    INSERT INTO EMPLOYEE_ATTENDANCE (
        EMPLOYEE_ID,
        ATTENDANCE_DATE,
        CLOCK_IN_TIME,
        CLOCK_OUT_TIME,
        STATUS,
        REMARKS,
        CREATED_AT
    ) VALUES (
        :P1_EMPLOYEE_ID,
        TO_DATE(:P1_DATE, 'YYYY-MM-DD'),
        TO_TIMESTAMP(:P1_CLOCK_IN, 'YYYY-MM-DD HH24:MI:SS'),
        TO_TIMESTAMP(:P1_CLOCK_OUT, 'YYYY-MM-DD HH24:MI:SS'),
        :P1_STATUS,
        :P1_REMARKS,
        CURRENT_TIMESTAMP
    );

    -- Optional: Commit if using autonomous transaction
    -- COMMIT;

    -- Display a success message in APEX
    APEX_UTIL.SET_SESSION_STATE('P1_SUCCESS_MSG', 'Attendance record saved successfully.');
EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        APEX_ERROR.ADD_ERROR(
            p_message => 'Attendance already exists for this employee on the selected date.',
            p_display_location => APEX_ERROR.C_INLINE_IN_FIELD,
            p_page_item_name => 'P1_DATE'
        );
    WHEN OTHERS THEN
        APEX_ERROR.ADD_ERROR(
            p_message => 'Unexpected error: ' || SQLERRM,
            p_display_location => APEX_ERROR.C_INLINE_IN_FIELD
        );
END;
