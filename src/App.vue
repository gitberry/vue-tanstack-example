<script setup>
import { h } from 'vue'
import { format } from 'date-fns'
import EditButton from '@/components/EditButton.vue'
import MetaButton from '@/components/MetaButton.vue'
import DisplayTrunc from '@/components/DisplayTrunc.vue'

import TableTanstack from '@/components/TableTanstack.vue'

import libraryindex from '@/MusicLibraryData.json'

// commented out columns I do not wish to display in the table
const columnsLibraryIndex = [
//{ accessorKey: 'id'                    , header: 'id'                    , enableSorting:false },
  { accessorKey: 'Edit'                  , header:  '',
    cell: ({ row }) => h(EditButton, { id: row.original.id })              , enableSorting:false },
//{ accessorKey: 'Title'                 , header: 'Title'                 , enableSorting:true },
  { accessorKey: 'Title', 
     header: 'Piece',
     cell: ({ row }) => h(DisplayTrunc, {
      displaydata: row.original.Title, 
      metadata: row.original.Title,
      dispmax: 33,
      }), 
      enableSorting:true },
//{ accessorKey: 'SubTitle'              , header: 'SubTitle'              , enableSorting:false },
  { accessorKey: 'Composer'              , header: 'Composer'              , enableSorting:true },
//{ accessorKey: 'ComposerPickerID'      , header: 'ComposerPickerID'      , enableSorting:false },
//{ accessorKey: 'Lyricist'              , header: 'Lyricist'              , enableSorting:false },
//{ accessorKey: 'Arranger'              , header: 'Arranger'              , enableSorting:false },
  { accessorKey: 'Publisher'             , header: 'Publisher'             , enableSorting:true },
//{ accessorKey: 'CopyrightNumber'       , header: 'CopyrightNumber'       , enableSorting:false },
//{ accessorKey: 'UserPermissionIfNotFGS', header: 'Legal', enableSorting:false },
//{ accessorKey: 'PricePerCopy'          , header: 'PricePerCopy'          , enableSorting:false },
//{ accessorKey: 'PricePerCopyAsOf'      , header: 'PricePerCopyAsOf'      , enableSorting:false },
  { accessorKey: 'Style'                 , header: 'Style'                 , enableSorting:true },
//{ accessorKey: 'Instrumentation'       , header: 'Instrumentation'       , enableSorting:false },
//{ accessorKey: 'Level'                 , header: 'Level'                 , enableSorting:false },
//{ accessorKey: 'ModifiedBy'            , header: 'ModifiedBy'            , enableSorting:false },
//{ accessorKey: 'ModifiedByUserId'      , header: 'ModifiedByUserId'      , enableSorting:false },
//{ accessorKey: 'ModifiedOn'            , header: 'Edited'                ,
//    cell: info => format(new Date(info.getValue()), 'MMM d, yyyy'),   
//    enableSorting:false },
// this was the challenge - allow the large screen users to have hover over abilities - but not
//   leave the mobile users in the lurch - the solution was a (i) icon for clicking AND hover abilities.
   { accessorKey: 'Meta', 
     header: 'Edited',
     cell: ({ row }) => h(MetaButton, {
      displaydata: format(new Date(row.original.ModifiedOn), 'MMM d, yyyy'), 
      metadata: 
       'Created:' + format(new Date(row.original.CreatedOn), 'MMM d, yyyy HH:mm:ss') + 
       ' By:' + row.original.CreatedBy +
       '\nEdited:' + format(new Date(row.original.ModifiedOn), 'MMM d, yyyy HH:mm:ss') + 
       ' By:' + row.original.ModifiedBy +
       '\nIn your timezone (UTC' + new Date().getTimezoneOffset()*-1/60 +' )',
       metaindicator: '&nbsp;&#9432;'
      }), 
      enableSorting:true },
//{ accessorKey: 'CreatedBy'             , header: 'CreatedBy'             , enableSorting:false },
//{ accessorKey: 'CreatedById'           , header: 'CreatedById'           , enableSorting:false },
//{ accessorKey: 'CreatedOn'             , header: 'CreatedOn'             , enableSorting:false },
];

</script>

<template>
  <div class="container mx-auto px-8 py-8">
    <!-- <TableOriginal /> -->
    <TableTanstack :data="libraryindex" :columns="columnsLibraryIndex" />
  </div>
</template>
