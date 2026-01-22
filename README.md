Date Validation 
Where End Date should not be Before the Start Date
<script type="text/javascript">

     //Defining Field IDs
    var START_DATE_ID = 37022;
    var END_DATE_ID   = 37023;

    // Defining Save button to Work after the Validation 
    $('#master_btnApply1, #master_btnApplyIcon, #master_btnSave1')
        .off('click')
        .removeAttr('onclick')
        .on('click', function () {

            var action = ($(this).attr('id').indexOf('Save') > -1) ? 'Save' : 'Apply';
            validateDates(action);
            return false; // stop default save
        });

// Defining Function for Validation (Start Date Must Not be Before the End Date)
    function validateDates(action) {
        var startDate = $CM.getFieldValue(START_DATE_ID, false);
        var endDate   = $CM.getFieldValue(END_DATE_ID, false);

        if (startDate && endDate && new Date(endDate) < new Date(startDate)) {

            WarningAlert(
                 '<b>Note:</b> Please provide an end date that comes after the start date',
                //'End Date must be the same as or later than Start Date.',
                 'Invalid Date Entry'   //POPUP HEADING
            );

            return; // block save
        }

        //Show the pop up to save
        ShowAnimationAndPostback('master$btn' + action);
    }

</script>
